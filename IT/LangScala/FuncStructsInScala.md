https://www.youtube.com/watch?v=Dsd4pc99FSY&list=PLFrwDVdSrYE6dy14XCmUtRAJuhCxuzJp0&index=1

#FSiS Part 1 - Type Constructors, Functors, and Kind Projector


scala> :k List
scala.collection.immutable.List's kind is F[+A]

```
trait Functor[F[_]] {
    def map[A, B](fa: F[A])(f: A => B): F[B]
}
```

Laws, type constructor for function (typed with A): `X => ?`, `import simulacrum._` reduces boilerplace.

```
@typeclass Functor[F[_]] {
}
```

It leads to
```
>Functor[List] = import of implicit
>import Functor.ops._ - import map function and friends.
```

self:
```
@typeclass trait Functor[F[_]] { self =>

  def compose[G[_]](implicit G: Functor[G]): Functor[Lambda[X => F[G[X]]] =
    new Functor[Lambda[X => F[G[X]]]]] {
    def map[A, B](fga: F[G[A])(f: A => B): F[G[B]] =
      self.map(fga)(ga => G.map(ga)(a => f(a)))
    }
}
```

`kind projector` plugin.
https://gist.github.com/pomadchin/60eeb514891217359bb047a4010b0c9a
https://github.com/mpilquist/structures

#FSiS Part 2 - Applicative type class
Functional pearls:
https://wiki.haskell.org/Research_papers/Functional_pearls
http://www.staff.city.ac.uk/~ross/papers/Applicative.pdf

    import simulacrum._
    
    @typeclass trait Applicative[F[_]] {
    def pure[A](a: A): F[A]

    def apply[A, B](fa: F[A])(ff: F[A => B]): F[B]
    }
Also trick `map4()` could be defined via `map2(tuple2, tupl2)`.

Applicatvie allows combine computations in parallel, not sequentially as it is for Monad transformers.

# FSiS Part 3 - Monad type class
https://www.youtube.com/watch?v=VWCtLhH815M&index=3&list=PLFrwDVdSrYE6dy14XCmUtRAJuhCxuzJp0

Analyse thread usage:
```
$ jps
2641 Main
2788 Jps
$jstack 2641
```

## Monad definition

    @typeclass Monad[F[_]] {self =>
      def pure[A](a: A): F[A]

      def flatMap[A, B](fa: F[A])(f: A => F[B]): F[B]
    
      override def apply[A, B](fa: F[A])(ff: F[A => B]): F[B] = flatMap[A => B, B](ff)((f: A => B) => map(fa)(f))

      override def map[A, B](fa: F[A])(f: A => B): F[B] = flatMap(fa)(a => pure(f(a)))
    }

Laws:
    trait MonadLaws[F[_]] {
      def flatMapAssociativity[A, B, C](fa: F[A], f: A => F[B], g: B => F[C]) = 
        f.flatMap(f).flatMap(g) =?= f.flatMap(a => f(a).flatMap(b => g(b)))

      def leftIdentity[A, B](a: A, f: A => F[B]) = 
        pure(a).flatMap(f) =?= f(a)

      def rightIdentity[A](fa: F[A]) = 
        fa.flatMap(identity) =?= fa
    }
