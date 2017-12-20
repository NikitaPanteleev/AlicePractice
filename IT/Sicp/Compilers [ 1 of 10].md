#Week 1: Introduction & the Cool Programming Language current chapter
- Compilers: program -> [Compiler] -> executable
- Interpretor: (program, data) -> interpreter -> output

1. Lexical analysis - divide program into tokens
2. Parsin
3. Sematic analysis - types, scope
4. Optimization
5. Code generation

application domains have different needs.
programming training is the dominant cost for programming language.

- Cool .cl

```
class Main {

  i: IO <- new IO;

  main(): Int { { i.out_string("Hello, world"); 1; } };

}
```

> coolc 1.cl
> spim 1.s

```
class Main inherits IO {
  main(): Object { self.out_string("Hello, world!\n")}

}
```
