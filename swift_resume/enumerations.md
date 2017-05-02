#####Enumerations in swift are first-class types in their own right.

```swift
	enum Planet {
		case red, blue
	}

	var flyToPlanet = Planet.red

	switch flyToPlanet {
		case .red:
			print("we re flying to the red planet")
		case .blue:
			print("we re flying to the blue planet")
	}
```

#####Associated values

```swift
	enum BarCode {
		case upc(Int, Int, Int, Int)
		case qrCode(String)
	}
```

As an alternative to associated values, enumeration cases can come prepopulated with default values (called raw values), which are all the same type.

Raw values can be strings, characters, or any of the integer or floating-point number types. Each raw value must be unique within its enumeration declaration.

#####Implicitly Assigned Raw Values

```swift
	enum Planet {
		case red = 1, blue
	}
```

If you define an enumeration with a raw-value type, the enumeration automatically receives an initializer that takes a value of the raw value’s type (as a parameter called rawValue) and returns either an enumeration case or nil. 

```swift
	let possiblePlanet = Planet(rawValue: 2)
```

Structures and Enumerations Are Value Types
A value type is a type whose value is copied when it is assigned to a variable or constant, or when it is passed to a function.

“Unlike value types, reference types are not copied when they are assigned to a variable or constant, or when they are passed to a function. Rather than a copy, a reference to the same existing instance is used instead.”

####Failable Initializers for Enumerations
You can use a failable initializer to select an appropriate enumeration case based on one or more parameters. The initializer can then fail if the provided parameters do not match an appropriate enumeration case.

####Overriding a Failable Initializer
Alternatively, you can override a superclass failable initializer with a subclass nonfailable initializer. This enables you to define a subclass for which initialization cannot fail, even though initialization of the superclass is allowed to fail.
