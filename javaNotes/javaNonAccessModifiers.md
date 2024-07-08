java, non-access modifiers

# Java Non-Access Modifiers

Java provides several non-access modifiers, which are used to provide additional information about the behavior of classes, methods, and variables beyond their access level. Here are the primary non-access modifiers in Java:

`static`
- Indicates that a member belongs to the class, rather than instances of the class. Static members can be accessed without creating an instance of the class.
- see `javaStatic.md`

`final`
- Used to declare constants. When applied to a class, it prevents the class from being subclassed. When applied to a method, it prevents the method from being overridden by subclasses. When applied to a variable, it makes the variable unchangeable after it is initialized.

`abstract` 
- Used in the declaration of a class to indicate that the class cannot be instantiated directly, and it must be subclassed. When applied to a method, it indicates that the method does not have an implementation in the class in which it is declared, and it must be implemented by subclasses.

`transient`
- Used in serialization. When an instance variable is declared as transient, its value is not serialized when the object is converted to a stream of bytes.

`volatile`
- Indicates that a variable may be changed unexpectedly by other parts of your program. It is used in multi-threaded programming to ensure that changes to variables are always visible to other threads.

`synchronized`
- Used to indicate that a method can be accessed by only one thread at a time. It's primarily used to prevent thread interference and memory consistency errors.

`native`
- Specifies that a method is implemented in native code using JNI (Java Native Interface).
