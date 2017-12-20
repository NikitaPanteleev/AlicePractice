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

### Tuples, Lists, Options, and Pattern Matching
```
# let a_tuple = ("hello", 42);;
val a_tuple : string * int = ("hello", 42)
# let languages = ["OCaml";"Scala";"Python"];;
# List.map languages ~f:String.length;;
# 1 :: [2; 3];;
- : int list = [1; 2; 3]
# [1; 2] @ [3; 4];;
- : int list = [1; 2; 3; 4]
# let my_favorite_language languages =
    match languages with
    | first :: the_rest -> first
    | [] -> "OCaml" (* A good default! *)
```

Recursive function `# let rec sum x`
```
#let divide x y =
    if y = 0 then None else Some(x / y);;
# let x = 7 in
  let y = x * x in
  x + y
  ;;
- : int = 56
```

### Records and variants
```
# type point = { x : float; y : float };;
# let p = { x = 3.5; y = 4.};;
# let sum { x; y} = x +. y;;
# List.exists (fun x -> x = 4) [3;4;5;];;
- : bool = true
```

### Mutable
Array: `let x = [| 2; 3 |];;` To refer an element use `x.(i)`;
Mutable record fields.
### Refs
`let x = { contents = 0 }` = `let x = ref 0`. to get the content `!x`

###For, while
for .. to .. do .. done

# Chapter 2. Variables and functions
