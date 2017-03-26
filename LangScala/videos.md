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


# BeeScala 2016: Ivan Topolnjak - Keeping it alive with Kamon
https://www.youtube.com/watch?v=4VZf3KKNOec

codehale limitation - not cheap in memory/cpu (??? proofs)
They use: https://github.com/HdrHistogram/HdrHistogram
- fixed memory cost
- constant time for recording
- blazingly fast (3-6 ns for recording).

TraceContext to measure execution between threads. Even tracing among
applications.

Jacob nielson:
What is fast
0.1s is fast - i am manipulating process
1s this is not me this is some processing
10s - not me 

KissMetrics:
47% of users want 2 seconds or less
40% of users will leave after waiting for more than 3 seconds
6 or 4 seconds for search.

Requirements:
- 95% less than 400ms
- 99% less than 1.2
- 100$ less than 4ms

# "How NOT to Measure Latency" by Gil Tene
https://www.youtube.com/watch?v=lJ8ydIuPFeU by Gil Tene
lattency 25$, 50%, 95$ - we don't know about rest 5%

http://latencytipoftheday.blogspot.ae/
42 requests per page, 5 click.
- 0.003% of users will not experience 95%
- 18% of users will experience 95% only once.

http://latencytipoftheday.blogspot.ae/2014/06/latencytipoftheday-most-page-loads.html
chance experiencing 99

*SHOW MAXIMUM VALUE*

So why not record 99999?
- dont need that level of perfection
- have not enough data.

While load testing.
- 1 request per second. but what if response takes more than 1
  second. Coordinated omission

During measurement
- slow operations measured only once (but maybe there was long
reindexing inside)
- slow operation could be outside

Service time vs Response time.
if you push above limit, your requests are in queue and you have to
wait and response time linearly increases.

Dont test above limit - it's like choosing bumper to sport car to
avoid crash. The limit itself matters. Find how fast is safe. WE dont
need insane rates
https://www.infoq.com/presentations/latency-response-time

gatling is the only one system which fixes coordinate emission problem.
