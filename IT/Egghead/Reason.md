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
 ```
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