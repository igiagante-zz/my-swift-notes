###Type aliases

Type aliases define an alternative name for an existing type. You define type aliases with the typealias keyword.

```swift
	typealias Audio = UInt
```

You can decompose a tuple’s contents into separate constants or variables

```swift
	let http404Error = (404, "Not Found")
	let (statusCode, StatusMessage) = http404Error
```

###Optionals
It should be used in situations where a value may be absent. An optional represents two posibilities: Either there is a value and it can be unwrapped 
the optional to get the value, or there isn't a value at all.

```swift
	var test: String?	
```

It uses **optional binding** to find out whether an optional contains a value, and if so, to make that value available as a temporary constant or variable. 

```swift
	if let constantName = OptionalName {

	}
```

Sometimes it is clear from a program’s structure that an optional will always have a value, after that value is first set. 
These kinds of optionals are defined as **implicitly unwrapped optionals**. You write an implicitly unwrapped optional by placing an exclamation mark **(String!)** rather than a question mark **(String?)** after the type that you want to make optional.

####Strings are values types

Swift’s String type is a **value type**. If you create a new String value, that String value is copied when it is passed to a function or method, or when it is assigned to a constant or variable. 

####Collections Types

Arrays are ordered collections of values. Set are unordered collections of unique values. Dictionaries are unordered collections of key-value associations.

An **array** stores values of the same type in an ordered list. The same value can appear in an array multiple times at different positions. 

A **set** stores distinct values of the same type in a collection with no defined ordering. 

A **dictionary** stores associations between keys of the same type and values of the same type in a collection with no defined ordering. 


####Tuples

You can use tuples to test multiple values in the same switch statement. Each element of the tuple can be tested against a different value or interval of values. Alternatively, use the underscore character (_), also known as the wildcard pattern, to match any possible value.

######Value Bindings
A switch case can bind the value or values it matches to temporary constants or variables, for use in the body of the case. 

######Where
A **switch** case use a **where** clause to check for additional conditions. 

```swift
	let anotherPoint = (2, 0)
	switch anotherPoing {

		case let(0, 0):
			print("(0, 0) is at the origin")

		case let(x, y):
			print("somewhere else at (\(x), \(y)")

		case let(x, y) where x == y:
			print("(\(x), \(y) is on the line x == y")
	}	
```

######Early exist
A **guard** statement, like an if statement, executes statements depending on the Boolean value of an expression. Unlike an if statement, a guard statement always has an else clause—the code inside the else clause is executed if the condition is not true. 

```swift
	guard let location = person["location"] else {
		print("where are you?")
		return
	}	
```

######Checking API Availability
You use an availability condition in an if or guard statement to conditionally execute a block of code, depending on whether the APIs you want to use are available at runtime. 

```swift
	if #available(iOS 10.0, iOS 9.3) {
	} else {
	}
```