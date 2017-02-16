https://www.tutorialspoint.com/java8/java8_overview.htm
>18 March 2014

New features:
- lambda expression
- method references
- default method
- new tools (as jdpes)
- stream api
- date time api
- Optional
- Nashorn JavaScript engine

# Lambda expressions
`parameter -> expression body`
- Optional type declaration
- Optional parenthesis around single parameter
- Optional curly braces if body contains single expression
- Optional return keyword if single expression

# Method Reference

```
new ArrayList<>(Arrays.asList("Nikita", "Ganesh")).forEach(System.out::println);
```

You can point methods using :: for
- static methods
- instance methods
- constructor using new Operator (TreeSet::new)

# Functional interfaces
https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html
`java.util.Function`

```
    BiFunction<String, String, Integer> length = (a, b) -> a.length() + b.length();
    System.out.println(length.apply("Hello", "World"));
```

# Default Methods
`default void print(){ .. }`

# Streams
- Sequence of elements; on demand, never stores events
- Source
- Aggregate operations (filter, map, limit, reduce, find, match.. )
- Pipelining (and collect() for final computation)
- Automatic operations 

Generating stream from standard collections using `stream()` or `parallelStream()`
Collectors: `.collect(Collectors.toList());`
Statistics: `.summaryStatistics();`

# Optional Class
https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html

# Nashorn JavaScript

# New Date/Time API
Problems of old datatime are 
- not thread safe
- poor design
- difficult time-zone handling

`java.time` Local or Zoned
`java.time.temporal.ChronoUnit` 
`java.time.Perio` for date based amount of time
`java.time.Duration` for time based amount of time
`java.time.temporal.TemporalAdjusters` for things like next Tuesday
`toInstant()` for backward compatibility

# base 64
http://stackoverflow.com/questions/201479/what-is-base-64-encoding-used-for
