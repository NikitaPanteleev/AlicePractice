#David Christiansen - Coding for Types: The Universe Patern in Idris - Curry On
https://www.youtube.com/watch?v=AWeT_G04a0A

It university of Copenhagen.

Red - constructor,
Blue - type constructor
Green - defined constant
Purple - bound variable

##The universe pattern

- Represent types with codes

`data Column = Text | Real | Integer`

- Interpret the codes as types

```
interpCol: Column -> Type
interpCol: Text -> String
interpСol: Real -> Double
interpCol: Integer -> Integer
```

### Sql example
Data schema and Type provider with side-effect.

Power of Pi, by Oury and Swierstra, ICFP 2008
