Extensions add new functionality to an existing class, structure, enumeration, or protocol type. This includes the ability to extend types for which you do not have access to the original source code (known as retroactive modeling). Extensions are similar to categories in Objective-C. (Unlike Objective-C categories, Swift extensions do not have names.).
Extensions can add new functionality to a type, they cannot override existing functionality.

```swift
	extension SomeType {
		//new functionality to add to SomeType goes here
	}	
```

```swift
	extension SomeType: SomeProtocol, AnotherProtocol {
		//implementation of protocol requirements goes here
	}	
```

> If it defines an extension to add new functionality to an existing type, the new functionality will be available on all existing instances of that type, even if they were created before the extension was defined.

####Computed Properties
Extensions can add computed instance properties and computed type properties to existing types.


```swift
	extension Double {
		var km: Double { return self * 1_000.0}
		var m: Double { return self * 1_000.0}
		var cm: Double { return self / 100}
	}	
	let aMarathon = 42.km + 195.m
```

####Initializers
Extensions can add new initializers to existing types. This enables you to extend other types to accept your own custom types as initializer parameters, or to provide additional initialization options that were not included as part of the type’s original implementation.

####Extensions can add new instance methods and type methods to existing type.

```swift
	func repetitions(task: () -> Void)
	{
		for _ in 0..<self {
			task()
		}
	}

	3.repetitions {
		print("test")
	}
```

Instance methods added with an extension can also modify (or mutate) the instance itself. Structure and enumeration methods that modify self or its properties must mark the instance method as **mutating**, just like mutating methods from an original implementation.