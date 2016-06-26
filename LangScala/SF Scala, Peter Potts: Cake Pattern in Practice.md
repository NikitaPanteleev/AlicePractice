# Cake pattern
http://www.youtube.com/watch?v=DysTHmpDgvk

< Interface >
< Implementation >
< Wiring >

# Reader monad
http://www.youtube.com/watch?v=ZasXwtTRkio

Inject ConfigFactory
Cons:
  - hidden dependencies
  - requires magic initialization step
  - (who closes connection? thread-local stuff?)

Solution:
 - Inversion of control == taking the argument
  `def setUserPwd(id: String, pwd: String, Connection: Connection):
  Unit`
But should we pass arguments all the way down?
 - Currying
 `def setUserPwd(id: String, pwd: String): Connection`

Wrap in case class:
`case class DB[A](g: Connection => A){def apply(c: Connection) =
g(c)}` + lift existing functions
`def map[B](f: A=> B): DB[B] = c => f(g(c))` + flatMap
Add constructor: `def pure[A](a: A): DB[A] = DB(c => a)`

# A little language
You provide KeyValueStore to the funcion i gave you and run it.
We need KWS[KWS[A]] => KWS[A]

`class Free[F[_], A](implicit F: Functor[F]) {}`
Two implementations:
`class Done[F[_]: Functor, A](a: A)`
`class More[F[_]: Functor, A](k: F[Free[F,A]])`
Functor is simply:
`trait Functor[F[_]] { def map[A,B](a: F[A])(f: A=> B): F[B] }`

old and busted => new hotness

Frameworks, factoris, magic init => functions from input to outputs
DI => little languages
Many implementations => Many interpreters of a language
of an interfact
