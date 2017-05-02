###Downcasting
Use the type check operator **(is)** to check whether an instance is of a certain subclass type. 

Where you believe this is the case, you can try to downcast to the subclass type with a type cast operator (as? or as!).
Because downcasting can fail, the type cast operator comes in two different forms. The conditional form, as?, returns an optional value of the type you are trying to downcast to. The forced form, as!, attempts the downcast and force-unwraps the result as a single compound action.

###Type casting for Any and AnyObject
* Any can represent an instance of any type at all, including function types.
* AnyObject can represent an instance of any class type.

Because downcasting can fail, the type cast operator comes in two different forms. The conditional form, as?, returns an optional value of the type you are trying to downcast to. The forced form, as!, attempts the downcast and force-unwraps the result as a single compound action.