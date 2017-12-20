[May Your Data Ever Be Coherent](https://www.youtube.com/watch?v=gVXt1RG_yN0)

Levels of incoherence

1. Buggy code
2. Some parts of code that we can prove as humans. These parts could be written such way that scala compile can prove them.
```
if (lst.empty) 0
else{
	val head = lst.head
	...
}
```
Improve them as pattern matching

3. Always reason by structure. Data flow is more typeable than control flow
4. tie your data to your branching
```
option match {
	case Some(v) => v
	case None => default
}
=
option.fold(some = {v => v}, none = default)
```

##Sequences
xs.length <- useless. It gives INT
The number of algorithms which depends on length of the list is small. They  all can be written on the board. MergeSort and quickSort are not the ones of them. quickSort is just stochastically faster if you use length.

5. Representation
Sequences are functions on iters. They are designed to be used only this way
6. Parametricity
Im thinking about ObjectData with fields of different types. And then represent compound type:Weight (Amenity)

Difference between reduce and fold [here](http://stackoverflow.com/questions/7764197/difference-between-foldleft-and-reduceleft-in-scala)