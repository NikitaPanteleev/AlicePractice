Voxxed days.
https://www.youtube.com/playlist?list=PLGsXDvjWzoeS2GjDvoifCloJPJNPawMzG

# G1 Garbage Collector Details and Tuning by Simone Bordet
# https://www.youtube.com/watch?v=Gee7QfoY8ys&index=17&list=PLGsXDvjWzoeS2GjDvoifCloJPJNPawMzG

G1 is replacement for CMS (concurrent map sweep)

G1 needs 2 parametrs:
- xmx - max heap size
- MaxGCPauseMillis = 250ms default

G1 divides the heapsize for 2048 regions and tags them as Eden, Survivor, Old generations and
- humongous region which occupies > 50% of size (byte[] or char[])

## how doed it work?
- jvm starts, G1 prepares Eden regions
- Eden regions are filled up
- When all Eden regions are full -> Young GC
- G1 tracks inter-generations pointers. (Map is in eden, after put() there is an object in "eden" region)
(Remember Set - pointers from outside; Card table - where are external pointers for these regions)
In every assignment it sents info about pointed and pointing objects into Dirty Card queue. In queue 4 zones:
When queue reached white zone, background threads are started which updated remembers set
When queue reached red zone, G1 asks application to do GC


Scala days:
# Options in Futures, how to unsuck them
https://www.parleys.com/tutorial/options-futures-how-unsuck-them
https://github.com/eamelink/flatten
Either[Future, Result, A] - to work with Future[Either[Result, A]
OptionT[Future, Int] - Future[Option[Int]]
