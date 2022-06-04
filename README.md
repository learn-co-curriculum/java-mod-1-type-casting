# Type Casting

## Learning Goals

- Understand strong typing
- Type cast in Java

## Introduction

Inheritance and strong-typing are two fundamental aspects of OOP in Java.
Strong-typing means that the Java compiler will not let you assign an un-related
type to a variable. For example, the following code will not compile:

```java
String mySring = 2;
```

Because the `String` class and the `int` primitive type or even the `Integer`
wrapper class do not inherit from each other.

## Type Casting in Java

Consider the following class hierarchy, which shows Java's "Object" class at the
root of all classes, and a few of the classes we have encountered in this
course.

_Note: Java's "Object" class is poorly named, because an "object" is usually an
instance of a class. But the class that all classes ultimately and implicitly
extend from is called "Object". In this course, as in most technical content, we
use the term "object" to refer to the instance of a class. We will make sure the
use the term "Java's Object class" when we are referring to the root class in
Java._

![Class Hierarchy](https://curriculum-content.s3.amazonaws.com/java-mod-2/type-casting/class-hierarchy.png)

In this diagram, the following hierarchy is represented:

1. Classes that do not extend any other class explicitly, therefore extends
   Java's Object class implicitly:
   1. String extends Object
   2. Number extends Object
   3. Animal extends Object
2. The following classes are "peer", i.e. they are subclasses of the same class,
   aka they extend the same class, in this case the Number class:
   1. Integer extends Number
   2. Double extends Number
   3. BigDecimal extends Number
3. The following custom classes that we created earlier in this module are also
   peers:
   1. Cat extends Animal
   2. Parrot extends Animal

Java supports two types of object conversion:

1. Downcasting
2. Upcasting

To understand how each work, let's consider a different way to phrase the
inheritance relationship between two classes. In our example, let's consider
that `Cat extends Animal`. Another way to say this is that "every cat is an
animal". The "is a" relationship is another way to say "every cat has all the
properties and actions of an animal".

When I declare a variable of type `Animal`:

```java
Animal myAnimal;
```

I can assign it an `Animal` value:

```java
myAnimal = new Animal();
```

Or I can assign it a `Cat` or `Parrot` value because since cats and parrots are
both animals, I can be confident that anything that an `Animal` object would
need will be part of the definition of a `Cat` or `Parrot` object:

```java
myAnimal = new Cat();
```

Note, however, that in this case the `myAnimal` variable is still considered by
your program to be of type `Animal`, so the variables and methods that are part
of the `Cat` type are not accessible using the `myAnimal` variable.

This is called "upcasting" because we are assigned an object an instance of a
class that is further "up" in the hierarchy, as depicted in the class diagram
above. And as you can see, it is done implicitly without needing any special
notation. It is a "safe" operation, i.e. it can never fail, because the `Animal`
holds less properties and has less methods than the `Cat` class, since the `Cat`
class extends the `Animal` class. So taking an `Animal` object and giving it all
the values a `Cat` object has guarantees that the `Animal` object will have all
the values it's expecting.

The reverse of this operation is called "downcasting", i.e. taking an instance
of a class higher in the hierarchy and assigning it the value of an instance of
a class lower in the hierarchy. That operation is not "safe" because it might
fail at runtime if the two types that you are trying to cast to one another are
not compatible.

To understand this better, we need to consider the previous example for
downcasting more closely. I will add a line of code to the previous example to
print the name of the class that my variable `myAnimal` is an instance of:

```java
Animal myAnimal = new Cat();
System.out.println(myAnimal.getClass().toString());
```

This produces the following output:

```
class Cat
```

As you can see, my `myAnimal` object is an object of type `Cat`, not of type
`Animal`. That's because there is a difference between the "compile-time" type
and the "runtime" type. At compile time, meaning when the code was written, the
type of the `myAnimal` variable was defined as `Animal`. However, when the
program runs, and an actual value is assigned to that variable, it's assigned a
value of type `Cat`, which is upcasting and is allowed, as we saw above.
Therefore, the runtime type of `myAnimal` is `Cat`.

This is a simple scenario where we can plainly see the runtime type, but there
are scenarios where the runtime type can vary based on things that happen in
your program or in other parts of the system you're putting together.

Since it is impossible for the compiler to anticipate all the permutations of
the runtime situations that your program will see, it's not possible for the
compiler to tell ahead of time whether a specific downcast will be possible or
not. Java deals with this uncertainty by requiring you, the programmer, to
explicitly downcast, which achieves two things:

1. It forces you to consider the logic in your own program and system to ensure
   that downcasting should work in your specific scenario
2. It allows you to put your explicit cast in a `try catch` block and catch the
   `ClassCastException` that the Java runtime will throw at runtime if your
   explicit cast is not actually possible

Here is the syntax for explicit casting:

```java
Animal myAnimal = new Cat();
Cat myCat = (Cat)myAnimal;
```

Note that the example above will compile and also run because `myAnimal`'s
runtime type is `Cat`, which is obviously compatible with the `myCat` variable.

Modifying the code as follows, however, will compile, but it will generate a
`ClassCastException` at runtime because you cannot cast from a lower class in
the hierarchy (`Animal`) to a higher class in the hierarchy (`Cat`). That is,
you can force the code to compile by adding the explicit downcast, but Java is
unable to do what you're asking it to do at runtime in this case because it
turns out that your `myAnimal` object does not have enough information in it to
give your `myCat` object everything it needs.

```java
Animal myAnimal = new Animal();
Cat myCat = (Cat)myAnimal;
```
