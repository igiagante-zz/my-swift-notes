##Value and Reference Types

Types in Swift fall into one of two categories: first, “value types”, where each instance keeps a unique copy of its data, usually defined as a struct, enum, or tuple. The second, “reference types”, where instances share a single copy of the data, and the type is usually defined as a class. In this post we explore the merits of value and reference types, and how to choose between them.


###What’s the Difference?

The most basic distinguishing feature of a value type is that copying — the effect of assignment, initialization, and argument passing — creates an independent instance with its own unique copy of its data

```swift
	struct S = { var data: Int = -1 }	
	var a = S()
	var b = a     // a is copied to b
	a.data = 42   // changes a, not b
	println("\(a.data), \(b.data)") // "42, -1"
```

Copying a reference, on the other hand, implicitly creates a shared instance. After a copy, two variables then refer to a single instance of the data, so modifying data in the second variable also affects the original, e.g.:

```swift
	// Reference type example
	class C = { var data: Int = -1 }	
	var x = C()
	var y = x     // x is copied to y
	x.data = 42   // changes a, not b
	println("\(x.data), \(y.data)") // "42, 42"
```