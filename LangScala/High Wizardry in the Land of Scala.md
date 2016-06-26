https://vimeo.com/28793245

Type system classify values.
Kind system classify types.
What does type system do?
values -> types -> kinds

`type List` :: * => *
`type Function1` :: (* x *) => *

Value level: `def id(x: Int) = x`
Type level:  `type Id[A] = A`

Value level: `def id(f: Int => Int, x: Int) = f(x)`
Type level: `type Id[A[_], B] = A[B]`