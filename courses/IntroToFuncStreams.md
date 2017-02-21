https://www.youtube.com/playlist?list=PLFrwDVdSrYE6PVD_p6YQLAbNaEHagx9bW
# Part 1

## Intro
fs2 - new name for scalaz streams
Library dependencies: libraryDependencies += "org.scodec" %%%
"scodec-bits" % "1.1.2"

*Simple example*
```
scala> Stream(1,2,3)
res0: fs2.Stream[Nothing,Int] = Segment(Emit(Chunk(1, 2, 3)))

```
Stream[Nothing, Int] - first type is side effect work, second is
emitting element type

`Stream.emit(List(1,2,3))`
`s1 interleave s2` for (1,2) & (3,4) it will be (1,3,2,4)
`s.zip(t)` - finishes when one of streams is out
`s.zip(t.repeat)` - when t is over, t is repeated again


Task is boxing value arount non-referential transparent computation
```
scala> Task.delay{println("here.."); System.currentTimeMillis}
res2: fs2.Task[Long] = Task

scala> res2.unsafeRun
here..
res3: Long = 1487016782578
```

1. `Task.now` - captures value and return it on each `unsafeRun`
2. `Task.delay` - reexecute on each `unsafeRun`
3.  given stratey like `implicit val strategy =
Strategy.fromFixedDaemonPool(8)` use `Task {...}`

`def eval[F[_], A](fa: F[A]): Stream[F, A]`

`Stream.eval().runLog` -> returns `F[Vector[A]]`

`Stream.eval().repeat` = `Stream.repeatEval()`

## IO
### Text
`io.readAll[Task](path, chunkSize)`

`f(a) == a |> f` and for function of type `Stream[F, A] =>
Stream[F, B]` we can use `src.through(f)`. This operation is called

Pipe = `type Pipe[F[_], -I, +O] = Strema[F, I] => Stream[F, O]`
`src.pipe(text.utf8Decode).pipe(text.lines)`

Sink = `type Sine[F[_], -i] = Pipe[F[_], -I, Unit]`
*NB* resources are cleaned up automatically even in case of excetioion


### Example with take n
```
import fs2._

def myTake[F[_], I](n: Int): Pipe[F, I, I] = h => {
  def go(n: Int): Handle[F, I] => Pull[F, I, Unit] = h => {
    if (n == 0) Pull.done
    else h.receive1{ case (a, h) => Pull.output1(a) >> go(n-1)(h)}
  }
  h.pull(go(n))
}

Stream.range(0, 1000).pure.through(myTake(5)).toList
```

`>>` is pure syntax for flatMap which ignores the input.

## Chunks
`Stream(1,2,3).chunks.toList = List(Chunk(1,2,3)`

`s.throughPure()` - just to overcome limitation that scalac doesn't
infer Nothing type.
