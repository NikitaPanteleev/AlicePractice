# https://www.youtube.com/watch?v=rTW9_p6Db_4
Pacific Northwest Scala 2013 Network I/O for a More Civilized Age: The New Akka I/O

NIO since java 1.4
Selector thread notifies tasks. Low level api where you should deregerster tasks.

Netty - rich api, but java api
ByteBuffer and akka.io introduces ByteString

ByteString can be compacted to one memory compact() - expensive operation
