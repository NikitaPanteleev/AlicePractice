# Prologue
https://github.com/realworldocaml/examples

# Chapter 1. A Guided Tour

### OCaml as calculator

```
# 3.5 +. 6.;;
- : float = 9.5
# 30_000_000 / 300_000;;
- : int = 100
# let x = 3 + 4;;
val x : int = 7
```

### Functions and Type Inference

```
# let even x = x mod 2 = 0;;
val even : int -> bool = <fun>
```

### Type Inference
Types can explicitly written:
```
# let sum_if_true (test : int -> bool) (x : int) (y : int) : int = ...
```

### Infering generic types:
Parametric polymorphism:

```
# let first_if_true test x y = if test x then x else y;;
val first_if_true : ('a -> bool) -> 'a -> 'a -> 'a = <fun>
```

