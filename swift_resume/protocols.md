A protocol defines a blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality. The protocol can then be adopted by a class, structure, or enumeration to provide an actual implementation of those requirements. *Any type that satisfies the requirements of a protocol is said to conform to that protocol.*

```swift

	protocol FirstProtocol {

	}

	class SomeClass: SomeSuperClass, FirstProtocol, AnotherProtocol {
		//implementation of protocol requirements goes here
	}	
```

A protocol can require any conforming type to provide an instance property or type property with a particular name and type. The protocol doesn’t specify whether the property should be a stored property or a computed property—it only specifies the required property name and type.

Getteable and setteable properties are indicated by writing **{ get set }** after their type declaration, and gettable are indicated by writing **{ get }**

```swift
	protocol SomeProtocol {
		// static properties
		static var staticTypeProperty: Int { get set }

		// instance properties
		var foo: Int { get set }
		var baz: Int { get }

		// static functions
		static func someTypeMethod()
		// instance functions
		func someInstanceMethod()
		// this functions modifies or mutate the instance it belongs to. 
		mutating func toggle()
	}	
```

####Initializer Requirements
Protocols can require specific initializers to be implemented by conforming types. 

```swift
	protocol SomeProtocol {
		init(someParameter: Int)
	}	

	class SomeClass: SomeProtocol {
		required init(someParameter: Int){
		}
	}
```

###Adding Protocol Conformance with an Extension
It can extend an existing type to adopt and conform to a new protocol, even if you do not have access to the source code for the existing type.


```swift
	class SomeClass {
	}

	protocol Descriptable {
		var description: String { get }
	}	

	extension SomeClass: Descriptable {
		var description: String { 
			print("I'm the SomeClass")
		}
	}
```

###Class-Only Protocols
It can limit protocol adoption to type class by adding the **class** keyword to a protocol's inheritance list. The **class** keyword must always appears first in protocol's inheritance list.

```swift
	protocol Descriptable: class, SomeInheritedProtocol {
		var description: String { get }
	}
```

###Protocol Extensions
Protocols can extended to provide method and property implementations to conforming types.

By creating an extension on the protocol, all conforming types automatically gain this method implementation without andy additional modification.

```swift
	extension RandomNumberGenerator {
		func randomBool() -> Bool {
			return random() > 0.5
		}	
	}

	let generator = Generator()

	print("Random Number \(generator.random())")
	// prints a random number

	print("Random Boolean \(generator.randomBool())")
	// prints a random boolean
```

###Adding Constraints to Protocol Extensions
When it defines a protocol extension, it can specify constraints that conforming types must satisfy before the methods and properties of the extension are available. You write these constraints after the name of the protocol you’re extending using a **where clause**.

```swift
	extension Array where Element == Int {

   func doSomething() {
       ... 
   }

   extension Stack where Element: Equatable {

   func isTop(_ item: Element) -> Bool {
       guard let topItem = items.last else {
       		return false;
       }
       return topItem == item
   }
```

###Providing Default Implementations
It can use protocol extension to provide a default implementation to any method or computed property requirement of the protocol. If a conforming type
provides its own implementation of a required method or property, that implementation will be used instead of the one provided by the extension.

```swift
	protocol ErrorHandler {
    	func handle(error: Error)
	}

	struct Handler: ErrorHandler {
    func handle(error: Error) {
        print(error.localizedDescription)
    	}
	}

	extension ErrorHandler {
    func handle(error: Error) {
        print(error.localizedDescription)
    	}
	}
}
```

####Why Not Base Classes?
Protocol extensions and default implementations may seem similar to using a base class or even abstract classes in other languages, but they offer a few key advantages in Swift:
* Because types can conform to more than one protocol, they can be decorated with default behaviors from multiple protocols. Unlike multiple inheritance of classes which some programming languages support, protocol extensions do not introduce any additional state.
* Protocols can be adopted by classes, structs and enums. Base classes and inheritance are restricted to class types.

In other words, protocol extensions provide the ability to define default behavior for value types and not just classes.

###Associated Types
An *associated Types* gives a placeholder name to a type that is used as a part of the protocol. The actual type to use for that associated type is not
specified until the protocol is adopted.

```swift
	protocol Container {
		associatedtype Item
		mutating func append(_ item: Item)
		var count: Int { get }
		subscript(i: Int) -> Item { get }
	}

	struct IntStack: Container {
		typealias Item = Int
		mutating func append(_ item: Item) {
			self.push(item)
		}
		var count: Int { 
			reutrn items.count
		}
		subscript(i: Int) -> Item { 
			return items[i]
		}
	}
}
```

* [Introducing Protocol-Oriented Programming in Swift 3](https://www.raywenderlich.com/148448/introducing-protocol-oriented-programming)
* [WWDC - Protocol-Oriented Programming in Swift](https://developer.apple.com/videos/play/wwdc2015/408/)
* [Protocol Oriented Programming is Not a Silver Bullet](http://chris.eidhof.nl/post/protocol-oriented-programming/)


