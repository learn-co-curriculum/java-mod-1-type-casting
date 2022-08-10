# Type Casting

## Learning Goals

- Explain what casting is in Java and how it works
- Talk about autoboxing and unboxing

## What is Casting?

**Type casting** is a process that converts one data type into another data
type. For example, we could convert an `int` into a `double`, but we may
experience issues if we were to convert a `double` into an `int`. Let's review
the different types of data types along with primitive versus reference
variables for a minute.

### Review of Variables

If we remember back from our Variable lesson, there were 7 different primitive
data types that we discussed:

- `boolean`
- `byte`
- `char`
- `int`
- `long`
- `float`
- `double`

Each of the primitive data types were of varying different sizes and held
different types of data: true/false values, single characters, whole numbers,
and fractional numbers.

Reference variables are different in that they refer to an object, like
instances of our `Bicycle` class or the `Student` class. A `String` data type is
also considered a reference variable.

## How Casting Works

To see how casting works, let us look back at the Math class' `sqrt()` method:

```java
double squareRoot = Math.sqrt(36);
```

The `sqrt()` method takes in a `double` data type, but here, we are providing it
an `int` data type with the value of 36. Since a `double` data type is actually
required, Java will automatically convert the `int` value, 36, to the `double`
value of 36.0 _before_ passing the parameter to the `sqrt()` method. The method
will then eventually return a double value of 6.0 and store it within the
`squareRoot` variable. This type of casting is referred to as **widening** or
**upcasting**.

We might be thinking why? And how can Java do this automatically? Remember how
our different primitive data types have sizes? Well an `int` is only 4 bytes
whereas a `double` is 8 bytes. Since the `int` is smaller, we can easily cast it
as a `double`. It's like taking the contents from a smaller box and placing them
in a larger box - we know all the contents will definitely fit because they
originally fit in a smaller box; hence the names widening and upcasting.

Here is a list of valid promotions that we can upcast data types to:

![type cast promotions](https://curriculum-content.s3.amazonaws.com/java-mod-1/type-casting/Type-Casting-Promotions.png)

[Reference: Java How To Program (Early Objects), Tenth Edition](https://learning.oreilly.com/library/view/java-how-to/9780133813036/ch06lev1sec7.html#ch06lev1sec7)

This list shows us all the ways we can upcast certain data types. As we saw, an
`int` can be upcast to a `double`, but we can also upcast it to a `long` or a
`float`. Also notice that the `boolean` data type is excluded from this list as
it is not considered to be a number in Java.

Now what if we want to go the other way? What if, for some reason, we decide to
go from a `double` to an `int`? We need to be careful when doing so since that
kind of casting truncates the decimal part of the `double` value. The same
could be said if we decided to go from a `long` to an `int`, we may truncate
part of the value when doing so. But it can be done!

```java
int squareRoot = (int) Math.sqrt(36);
```

Since we know that `Math.sqrt(36)` will return a `double` with the value 6.0,
we can cast the 6.0 to an `int` data type by placing `(int)` in front of the
value we want to cast. This will force the compiler to jam the value of a
`double` into an `int`. This means the value of 6.0 will then become a 6 and be
assigned to the `int squareRoot`. This type of casting is referred to as
**narrowing** or **downcasting**.

As stated before, we need to be careful when downcasting because we could be
truncating the size so much that we lose information. Let's compare this to our
box example. If we take the contents out of a larger box and place them in a
smaller box, we do not know for sure if all the contents will fit. If the
contents do not all fit  in the smaller box, we may not be able to put all the
items into the smaller box - leaving some items completely out of a box.

## Autoboxing and Unboxing

Let's go back to the difference between primitive types and reference types
again. Reference variables refer to an object in Java. But wouldn't it be nice
if we could treat our primitive variables the same way? As an object instead?
In Java, there exist a couple of wrapper classes to do just that! A **wrapper**
**class** is a class whose object contains primitive data types so that we can
use them as objects. Consider the following table of primitive data types and
the equivalent wrapper class:

| Primitive Data Type | Wrapper Class |
|---------------------|---------------|
| `boolean`           | `Boolean`     |
| `byte`              | `Byte`        |
| `char`              | `Character`   |
| `int`               | `Integer`     |
| `long`              | `Long`        |
| `float`             | `Float`       |
| `double`            | `Double`      |

We can initialize a wrapper object in a similar way that we would initialize a
primitive data type:

```java
Integer x = 8;
Double y = 18.50;
```

Now what if we have a primitive data type, but we want to use it like an object?
Can we cast it to its corresponding wrapper class? The answer is yes - but this
is a special kind of cast. **Autoboxing** is the automatic conversion between a
primitive and its wrapper class. Let's look at an example!

```java
int a = 8;
double b = 18.50;

// Autoboxing
Integer x = a;
Double y = new Double(b);
```

Notice how we can either convert the primitive to its wrapper object by directly
assigning the primitive to the wrapper object, or using the syntax
`Object object = new Object()` and feeding the wrapper class the primitive value
as a parameter.

**Unboxing** is the opposite of autoboxing in that it converts an object of its
wrapper class to its matching primitive. This is also an automatic conversion
just like autoboxing!

```java
Integer x = 8;
Double y = 18.50;

// Unboxing
int a = x;
double b = y;
```
