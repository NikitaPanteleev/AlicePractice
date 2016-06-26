http://www.pluralsight.com/courses/understanding-java-vm-memory-management

# Introduction

Promise about living object.
Types of GC:

 - do nothing.
 - reference counting (addref, release)
 - mark and sweep.
   two phases: mark all live objects and delete not uses. leave us
   with fragmented memory.
 - copying: mark, sweep and rearrange memory.
 - generational. if object survives for one GC, gc will not look at it
   for while, because it's probably will survive for long.
 - incremental - look at all memory all the time.

##reference counting
Circle references - two objects can reference each other, but no outer
pointer to them

##mark and sweep
Start from the root object and mark all references. Dead circles are removed.
## copying
keep two areas of memory
## generarional
 2 or more generations of objects.
 sun.misc.Unsafe

# How Garbage Collection Works in the Oracle JVM
 - Stop the world events.
 - memory fragments.
 - throughtput
 - different GCs.
 - multicore GCs.

## generations
 - young
   *  eden
   *  2 surviver spaces which are swapped every run
 - old generations - promote code here then young is full.
 - permanent

Die young or live forever.
*minor GC and major GC* minor + major = Full.
options to allocate object of size n directly to old generation.
Each thread allocates its own Thread Local Allocation Buffer (TLAB) ->
no locking required.

*Roor* - stack, static variables,JNI, and..
references from old generations -> write barier and card table where
we store object that reference to young generation.

Options:

- serial collector.
    *  single threaded, mark and sweep, ok for small apps running on the
     client
 - parallel collector
    * multiple threads for minor, single for major
    * use on services
 - parallel old collector
    * mutiplre thread for minor, major
    * preferred over parallel
 - concurrent mark and sweep
    * no longer bump the pointer, it allocates objects in fragmented
      memory
 - G1 garbage collector - compacting collectore - replacement for
   concurrent mark and sweep
    * run on multi-processor server, it breaks heap into regions,
      evacuations between regions.
# Garbage collection tools
 - Java MX Bean `java.lang.management.GarbageCollectorMXBean`
 - jstat -option <pid> <interval> <count>
  use `$ jps` to find all processes
  Example: jstat -gccapacity pid
 - Visual VM and install plugin VisualGC
  `$ jvisualvm`

#Java Reference Classes
 - strong references
 - strong -> soft -> weak -> phantom
 - weak pointed objects are collected if memory pressure
  * metadata to another type
  * weakHashMap weak key -> metadata
 - soft
  * can be used for caching
 - phantom reference
  * interaction with gc - finalize

ReferenceQueues
