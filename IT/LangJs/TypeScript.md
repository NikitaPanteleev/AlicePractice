#Motivation video
https://www.youtube.com/watch?v=e3djIqAGqZo
Typescript: Angular 2's Secret Weapon - Dan Wahlin

# install
Install typescript, jest and typings:
```
npm install typings --global
typings install dt~jest --global --save
```

#Docs
https://www.typescriptlang.org/docs/handbook/variable-declarations.html
`let` has lexical-scope.

# Handbook

## Types
number, string, boolean, enum, object
String supports `${ } `

## Variable declaration
let & const

Destructing: 
`let [first, ...rest] = [1, 2, 3, 4];`
`let [, second, , fourth] = [1, 2, 3, 4];`

```
let o = {
    a: "foo",
    b: 12,
    c: "bar"
};
let { a, b } = o;
```
Giving new name:
`let { a: newName1, b: newName2 } = o;`

Readonly, const, optional params.