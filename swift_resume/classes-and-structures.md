####Structures and Enumerations Are Value Types
A value type is a type whose value is copied when it is assigned to a variable or constant, or when it is passed to a function.

####Classes Are References Types
Unlike value types, __reference types__ are not __copied__ when they are assigned to a variable or constant, or when they are passed to a function. Rather than a copy, a reference to the same existing instance is used instead.

####Identity Operators

* Identical to (===)
* Equal to (==)

* "Identical to" means that two constants or variables of class type refer to exactly the same class instance.
* "Equal to" means that two instances are considered "equal" or "equivalent" in value, for some appropiate meaning of "equal", as defined by the type's designer.


####Choosing Between Classes and Structures
However, Swift only performs an actual copy behind the scenes when it is absolutely necessary to do so. 

In Swift, many basic data types such as String, Array, and Dictionary are implemented as structures. 

In its simplest form, a stored property is a constant or variable that is stored as part of an instance of a particular class or structure. Stored properties can be either variable stored properties (introduced by the var keyword) or constant stored properties (introduced by the let keyword).

####Stored Properties of Constant Structure Instances
If you create an instance of a structure and assign that instance to a constant, you cannot modify the instance’s properties, even if they were declared as variable properties.

The same is not true for classes, which are reference types. If you assign an instance of a reference type to a constant, you can still change that instance’s variable properties.

A **lazy stored** property is a property whose initial value is not calculated until the first time it is used. 

It must always declare a lazy property as a variable (with the var keyword), because its initial value might not be retrieved until after instance initialization completes. 

####Computed Properties
In addition to stored properties, classes, structures and enumerations cand defined computed properties, which do not actually store a value. Instead, they provide a getter and an optional setter to retrieve and set other properties and values indirectly.


```swift
	struct Cuboid {
	var with = 0.0, height = 0.0, depth = 0.0
	var volume: Double {
		return with * height * depth
	}	
```

It must declare computed properties—including read-only computed properties—as variable properties with the var keyword, because their value is not fixed. 

####Property Observers
Property observers observe and respond to changes in a property’s value. Property observers are called every time a property’s value is set, even if the new value is the same as the property’s current value.

It has the option to define either or both of these observers on a property:

* **will set** is called just before the value is stored.
* **did set** is called immediatly after the new value is stored.

```swift
	class Car {
	var color: String {
		willSet(color) {
		}
		didSet(color) {
		}
	}
```

####Type Properties
It can also define properties that belong to the type itself, not to any one instance of that type. 

```swift
	struct SomeStructure {
		static var storedTypeProperty = "Some value."
		static var computedProperty: Int {
			return 1
		}
	}

	enum SomeEnumeration {
		static var storedTypeProperty = "Some value."
		static var computedProperty: Int {
			return 1
		}
	}

	enum SomeClass {
		static var storedTypeProperty = "Some value."
		static var computedProperty: Int {
			return 1
		}
		class var overrideableComputedTypeProperty: Int {
			return 107
		}
	}	
```

####Modifying Value Types from Within Instance Methods
Structures and enumerations are value types. By default, the properties of a value type cannot be modified from within its instance methods.
However, if you need to modify the properties of your structure or enumeration within a particular method, you can opt in to **mutating behavior** for that method. 

```swift
	struct Point {
		static var x = 0.0, y = 0.0
		mutating func moveBy(x deltaX: Double, y deltaY: Double) {
			x += deltaX
			y += deltaY
		}
	}	
```

It can also define methods that are called on the type itself. These kinds of methods are called type methods. You indicate type methods by writing the static keyword before the method’s func keyword. Classes may also use the **class** keyword to allow subclasses to override the superclass’s implementation of that method.

```swift
	struct SomeClass {
		class func someTypeMethod() {

		}
	}
	SomeClass.someTypeMethod()
```

####Subscripts
Classes, structures, and enumerations can define subscripts, which are shortcuts for accessing the member elements of a collection, list, or sequence. 

```swift
	subscript(index: Int) -> Int {
		get {
		}
		set(newValue) {
		}
	}
```
Subscripts can take any number of input parameters, and theses input parameters can be of any type. Subscripts can also return any type.

####Overriding
A subclass can provide its own custom implementation of an instance method, type method, instance property, type property, or subscript that it would otherwise inherit from a superclass. This is known as overriding.

#####Preventing Overrides
It can prevent a method, property, or subscript from being overridden by marking it as **final**. Do this by writing the final modifier before the method, property, or subscript’s introducer keyword (such as final var, final func, final class func, and final subscript).

###Initializers
If a property always takes the same initial value, provide a default value rather than setting a value within an initializer. The end result is the same, but the default value ties the property’s initialization more closely to its declaration. 

####Parameter Names and Argument Labels
As with function and method parameters, initialization parameters can have both a parameter name for use within the initializer’s body and an argument label for use when calling the initializer.

Properties of optional type are automatically initialized with a value of nil, indicating that the property is deliberately intended to have “no value yet” during initialization.

Swift provides a default initializer for any structure or class that provides default values for all of its properties and does not provide at least one initializer itself.

####Failable Initializers
A failable initializer creates an optional value of the type it initializes. 

```swift
	struct Animal {
		let species: String
		init?(species: String) {
			if species.Empty { return nil }
			self.species = species
		}
	}
```