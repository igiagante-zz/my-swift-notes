###The Role of Mutation in Safety

One of the primary reasons to choose value types over reference types is the ability to more easily reason about your code. If you always get a unique, copied instance, you can trust that no other part of your app is changing the data under the covers. This is especially helpful in multi-threaded environments where a different thread could alter your data out from under you. This can create nasty bugs that are extremely hard to debug.

Because the difference is defined in terms of what happens when you change data, there’s one case where value and reference types overlap: when instances have no writable data. In the absence of mutation, values and references act exactly the same way.

You may be thinking that it could be valuable, then, to have a case where a class is completely immutable. This would make it easier to use Cocoa NSObject objects, while maintaining the benefits of value semantics. Today, you can write an immutable class in Swift by using only immutable stored properties and avoiding exposing any APIs that can modify state. In fact, many common Cocoa classes, such as NSURL, are designed as immutable classes. However, Swift does not currently provide any language mechanism to enforce class immutability (e.g. on subclasses) the way it enforces immutability for struct and enum.

###How to Choose?

So if you want to build a new type, how do you decide which kind to make? When you’re working with Cocoa, many APIs expect subclasses of NSObject, so you have to use a class. For the other cases, here are some guidelines:

Use a value type when:

* Comparing instance data with == makes sense
* You want copies to have independent state
* The data will be used in code across multiple threads
* Use a reference type (e.g. use a class) when:
* Comparing instance identity with === makes sense
* You want to create shared, mutable state

In Swift, Array, String, and Dictionary are all value types. They behave much like a simple int value in C, acting as a unique instance of that data. You don’t need to do anything special — such as making an explicit copy — to prevent other code from modifying that data behind your back. Importantly, you can safely pass copies of values across threads without synchronization. In the spirit of improving safety, this model will help you write more predictable code in Swift.

###Identity vs Equality

Because reference types may refer to the same instance, identity (===) makes sense. So in our initial Person example, if we want to know if my neighbor is Bob, we want to know if it is the exact same person, not just any person with the same name and age.

For value types, since we are creating new instances whenever they are copied, we need to be able to compare them not by their identity, but by their value. So in this case, it generally makes sense to compare value types using equality (==) instead.

If I have a 20 dollar bill and someone takes it and replaces it with another 20 dollar bill, I might not even notice. The identity of the bill isn’t important, the value is.

When thinking about your model and trying to figure out which type to use, see if it makes sense to compare the object with identity or equality. If it is clearly one or the other, it can make the decision between reference and value types easy.

This is another argument against including reference types as properties on a value type, as this makes it hard to compare the value types with equality. If you are unable to compare its properties using equality, it makes it hard to make the object itself Equatable.