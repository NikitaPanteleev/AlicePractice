https://www.youtube.com/watch?v=Dsd4pc99FSY&list=PLFrwDVdSrYE6dy14XCmUtRAJuhCxuzJp0&index=1

#FSiS Part 1 - Type Constructors, Functors, and Kind Projector
```
scala> :k List
scala.collection.immutable.List's kind is F[+A]

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
https://github.com/mpilquist/structures
