# http://www.youtube.com/watch?v=8fC2V9HX_m8
# Advanced Stream Processing in Scala
##Process1: a 1-input stream processor
```
sealed trait Process1[I, O]

case class Halt[I,O]() extends Process1[I,O]
case class Emit[I,O](
  head: Seq[O],
  tail: Process1[I,O] = Halt[I,O]());
case class Await[I,O](
  recv: I => Process1[I,O],
  fallback: Process1[I,O] = Halt[I,O])()


def sum: Process1[Double, Double] = {
  def go(acc: Double): Process1[Double, Double] =
    Await[Double, Double]((d:Double) => Emit(Seq(d + acc), go(d+acc)))
  go(0.0)
}
```

## Abstracting over the context.
Deal with requests: Process[F[A], O]
```
case class Await[F[_], A, O](
  req: F[A], recv: A => Process[F,O],
  fallback: Process[F,O],
  onError: Process[F,O]) extends Process[F,O]
```
## Effectful sinks and channels.
`type Sink[F[_],O] = Process[F, O => F[Unit]]`
`type Channel[F[_], I, O] = Process[F, I => F[O]]`
## Nondetermenism.
Representing nondeterminism explicitly
`type Wye[I,I2,O] = Process[Y[I,I2]#f, O]` - either I or I2 value is
taken.
## Distributed execution.

```
scala> Stream(1,2,3).repeat.covary[Task]
res5: fs2.Stream[fs2.Task,Int] = append(Segment(Emit(Chunk(1, 2, 3))), Segment(Emit(Chunk(()))).flatMap(<function1>))

scala> res5.open
res6: fs2.Pull[fs2.Task,Nothing,fs2.Handle[fs2.Task,Int]] = Pull
```
`Pull[Task, Nothing, Handle[Task, Int]]` - side-effect type, out type
and type we can map over.

When you `open` stream you get `Pull`, when you `close` stream you get
back stream.
```
scala> res5.open.flatMap(h => Pull.output1(42)).close.runLog.unsafeRun
res9: Vector[Int] = Vector(42)
```

## interleave
Stream(1,2,3) interleave Stream(4,5,6) -> 1,4,2,5,3,6
type is `type Pipe2[F[_], -I1, -I2, O] = (Stream[F. I1], Stream[F, I2])
=> Stream[F, o]`

`evalMap` for side effect work and `unsafeRunFor(5.seconds)` to run
