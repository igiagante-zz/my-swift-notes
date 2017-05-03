###ARC (Automatic Reference Counting)

#####Weak References
A *weak reference* is a reference that does not keep a strong hold on the instance it refers to, and so does not stop ARC from disposing of the referenced instance. 

#####Unowned References
Like a weak reference, an *unowned reference* does not keep a strong hold on the instance it refers to. Unlike a weak reference, however, an unowned reference is used when the other instance has the same lifetime or a longer lifetime. 

However, there is a third scenario, in which both properties should always have a value, and neither property should ever be nil once initialization is complete. In this scenario, it’s useful to combine an unowned property on one class with an implicitly unwrapped optional property on the other class.

###Resolving Strong Reference Cycles for Closures
It should define a *capture list* as part of the closure's definition.


```swift
	lazy var someClosure: () -> String = {
		[unowned self, weak delegate = self.delegate!] in
		// closure body goes here
	}
```