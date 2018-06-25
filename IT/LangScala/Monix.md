https://www.youtube.com/watch?time_continue=42&v=JFbYQGG2Nb4

```
type Iterator[+A] = 
  () => Option[Either[Throwable, A]]

type Iterable[+A] = 
  () => Iterator[A]
```

and reverse is

```
type Observer[-A] = 
  Option[Either[Throwable, A]] => ()

type Observable[] = 
  Observer[A] => A
```