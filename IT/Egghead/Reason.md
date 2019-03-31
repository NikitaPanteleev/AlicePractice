# Installation
https://reasonml.github.io/docs/en/installation

+ reason cli:
```
npm install -g reason-cli@latest-macos
```

`rtop` is cli tool.

Syntax tree is usual: 

## Basic datatypes
`+ - / * ` - for integers
` +. -. /. *.` -for floats
`"Hello,  ++ "world"` - string concatenation
`();` - type of unit.

## Let bindings
`let binding: type definition = result of the evaluated code;`
`type list = list(sting)` - type alias

## scope
inner scope is not accessible from outside as expected.

## If/Else and switch
`var a = if (true) {"Good Morning"} else {"Hello"};`  - if is an expression, not a statement

Switch:
```
switch (<value>) {
| <pattern1> => <case1>
| <pattern2> => <case2>
...
}
```

## Records:
```
type person = {
  name: string,
  age: int,
};
let tim = { 
  name: "Tim",
  age: 52,
}
tim.name
```
 - Restructiring: `let {name: timsName} = tim` give us `let timsName: string = "Time";`
 - Spread operator:
```
let evenOlderTim = {
  ...olderTim, 
  age: olderTim.age + 1,
};
```
 - Mutable fieds:
```
type animal = {
  species: string,
  mutable scary: bool,
};
```
 - Punning for record creation:
 ```
 type coordinates = {
  x: int,
  y: int,
};
type circle = {
  coordinates,
  radius: int,
};
```
`coordinates` name and type coincides, so we can skip type.

  - public fields:
```
let anna = {
  pub name = "Anna";
  pub eyecolor = "brown";
};
let anna: {. eyeColor: string, name: string} = <obj>;
Reason # anna#eyeColor;
- : string = "brown"
```

## Variants and pattern matching

Variants are known as tagged unions in Computer Science.
```
type item = 
  | Note(string)
  | Todo(string, bool);
```

## type Option
`None` and `Some()`, and also `Some(x)` is the same as `?x`
`(x:?) => `


## functions
`let add = (x: int, y: int) : int => x + y;`
Named parameters:
```
let name = (~firstName, ~latName) => firstName ++ " " ++ lastName;
name(~firstName="Jane", ~lastName="Doe");
```
1. Convention to use default arguments and labeled parameters is to add () as the end argument.
2. `_item` or `(_)` for not used arguments.
3. Recursive Functions `let rec functionName`
4. Mutual recursive functions: `let func1 and func2`

## pipe operators
```
let info = String.capitalize(String.lowercase("ALERT")); // "Alert"
let info = "ALERT" |> String.lowercase |> String.capitalize; // "Alert"
```
## Tuples, Lists and Arrays in Reason
Tuple: `(a,b)`; `fst, snd` - to access 1, 2 arguments, other through desctructiring.
List: `[ , , , ,]` - immutable. `@` concatenets, `[0, ...[1,2]]`, access via switch or `List.nth(lst, index)`
Array: `[|a, b|]`, access via `a[i]` and assign `a[i] = 7` and `Array.map` + other std functions.

## Reference Equality (===) vs Structural (deep) Equality (==)

## Pattern matching
Like in oCaml, Scala. And for arrays:
```
switch ([|"a", "b", "c"|]) {
| [|"a", "b", _|] => print_endline("a, b and something")
| [|_, "x", "y"|] => print_endline("something, " ++ x ++ y)
| _ => print_endline("An Array")
};
```
We can combine multiple cases:
```
switch (2) {
| 1 | 2 | 3 => "between 0 and 4"
```
Or:
```
| Error(500 | 501 | 502) => "A server error occurred."
| Error(code) when isServerError(code) =>
| 0 as x =>
```
Ternary sugar is available.

## Type parameter
`let myList: list(string)` and generally: `type coordinate('a) = ('a, 'a);`

## Mutable let bindings in Reason
```
let foo = ref(5);
foo := 6;
foo^;
```

## Exceptions in Reason
```
exception Inputclosed(string);
raise(inputClosed("the stream has closed"));
```
You can also pattern match exceptions.

## Imperative Loops (for & while)
`for (x in 8 to 2)` or `for (x in 8 downto 2)`, `while (x^ < 5)`

## Modules
`module VideoGame = {include Game; };`
Also possible to define types
`module type Company{}` and `module TradingCompany: Company = {}`,
types are provided in separate file `.rei`