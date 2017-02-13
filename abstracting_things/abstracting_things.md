<!-- toc -->

# Abstracting Things

Abstracting things allows us to establishing a level of complexity on which a person interacts with the system. The more complex details are hidden below the current level. The user works with an idealized interface (usually well defined) and can add additional levels of functionality that would otherwise be too complex to handle.

> The essence of abstractions is preserving information that is relevant in a given context, and forgetting information that is irrelevant in that context.
>
> John V. Guttag (2013-01-18)

Take for example a programmer that is developing a calculator application. This programmer might not be interested in the way numbers are represented in the underlying hardware (e.g. whether they're 16 bit or 32 bit integers). The boundary where those details have been suppressed, we can state that they have been abstracted away. The programmer now just has numbers with which he can work.

All programming languages provide abstractions. The actual quality of the abstractions will determine the complexity of the problem you are able to solve. Try writing an MMORPG game using nothing but assembler.

In fact assembly language is an abstraction for machine code which is an abstraction of the actual hardware of a computer system.

![Assembler is an abstraction of Machine Code [^1]](img/assembler_abstraction.jpg)

[^1]: Source http://www.androidauthority.com/assembly-language-and-machine-code-678230/

Many imperative languages that followed (such as Fortran, C, Pascal, ...) were another level of abstraction introduced on top of the assembly language.

![Multiple Layers of Abstraction](https://www.lucidchart.com/publicSegments/view/9795cc73-acd7-478a-a1e0-3bc66b19496c/image.png)

So called imperative languages are a big improvement over the low-level assembly language. They do however still require that the programmer thinks in terms of the structure of the computer rather than in terms of the structure of the problem.

These languages chose a particular views of the world of problems. While they are good solutions to particular classes of problems, they do become awkward when you step outside their domain.

The object oriented approach takes it all a step further by given the programmer the ability to represent the elements from the problem space in the solution space. This representation is general enough so that it is not constrained to any particular type of problem. Elements in the problem space are represented in the solution space as **objects**.

This also allows the programmer to express the solution using the lingo of the problem space by adding types of objects. In other words, reading the code that describes the solution uses the same words that also express the problem. Of course a programmer will also be able to create objects that are not directly related to the problem space.

Alan Kay, a renowned computer scientist, listed the five characteristics of Smalltalk, the first successful object oriented programming language and one of the languages on which C++ is based. They summarize the characteristics that represent a pure approach to object oriented programming:

1. **Everything is an Object.** An object contains both data and behavior (this is  also knows as *encapsulation*). It keeps state and can satisfy outside requests by performing operations on itself. You can basically create objects of any conceptual component in the problem you are trying to solve (people, buildings, lists, records, ...).

2. **A program is a bunch of objects telling each other what to do by sending messages.** To make a request of an object, a message needs to be send to it. This will call a certain method of that particular object.

3. **Each object has its own memory made up of other objects.** Think of this as creating another type of object by packaging together other objects, this will later be seen as what is called *composition*. This allows us to hide complexity behind the simplicity of objects. In other words, objects allows to create new levels of abstraction.

4. **Every object has a type.** Or in OOP lingo, each object is an *instance* of a *class* in which class actually is a synonym of type. A class defines what messages can be send to the objects of that particular class.

5. **All objects of a particular type can receive the same messages.** This is a bit more complex than it sounds. Basically, an object of type *circle* is also an object of type *shape*, meaning that a circle object will be guaranteed to also accept shape messages. This is where *polymorphism* comes into play: meaning you can write code that talks to shapes and automatically handles other objects that also fit the description of shapes, such as circles. This *substitutability* forms one of the most powerful concepts of OOP.

## The interface of an Object

Aristotle was one of the first to study the concept of *type*. He spoke of *the class of fishes and the class of birds*. The idea is that each object is unique (because of their state) but is also part of a class of objects that share characteristics and behavior.

Objects satisfy the requests that are being send to them (ex. draw something on the screen, complete a bank transaction, download a file from the Internet, ...). In practice, a *contract* is created between the creator of the class and the user of the class, which defines what messages can be send to a certain class of objects. This contract is realized by the **public interface** of the objects. In other words the interface of a class establishes what requests you can make to its objects.

There must however be code somewhere to satisfy the requests. This along with the *hidden data* comprises the *implementation* of the class.

So summarized: a type (class) has a method associated with each the possible requests (the interface) that can be made to the objects of that class. When a message is send to an object, the corresponding method is called, and the object figures out what to by executing the code that forms the implementation of that method.

Note that the interface of the class only consists of the public portions of the methods. The methods and attributes that are private are not considered part of the **public interface** of the class. Because of this, some programmers will leave out the private parts of the class from the UML class diagram, as they are considered private details to the actual implementation of the class.

## Reusing implementation

Once a class has been created and hopefully tested it should ideally represent a useful unit of code.  In this case it begs to be reused and not go to waste. It also turns out that code reuse is one of the main advantages of object oriented programming.

> #### Warning::Reuse and DRY
>
> Code reuse is not, as some understand it to be (students in particular), the ability to be copy pasted from one part inside your program to another! This is actually *code duplication* and is considered bad practice. The DRYness (DRY - Don't Repeat Yourself) of once code is one of the indicators of the maintainability of that code.

Multiple ways exist to reuse a class:

* **Association**: Just use the objects of a class.
* **Composition/Aggregation**: Build classes that consist of other objects.
* **Inheritance**: Extend an existing class by inheriting from a base class.

## Reusing the Interface - Inheritance

The concept of an object is a convenient tool. It allows you to package data and functionality together by concept. It would be a pity if one had to go through all the trouble to create a class and then be forced to create a brand new one even if it is very similar to the other one.

It's much more convenient to be able to clone classes and make additions and modifications to this clone. This is exactly what **inheritance** allows us to do. Inheritance lets you reuse classes as new classes that might have a similar functionality. On top of this, if the original class is modified, these modifications are also reflected in the clones.

Inheritance is visualized in a UML class diagram using an arrow from the new class (called the **derived, inherited, child or sub class**) to the original class (called the **super, base or parent class**).

![UML class diagram of Inheritance](https://www.lucidchart.com/publicSegments/view/6618e1b2-c49c-4f55-affc-e5aaf9a9fdc8/image.png)

Object-oriented programming allows classes to inherit commonly used state and behavior from other classes. In an inheritance hierarchy the base class contains all the common characteristics and behaviors of the derived classes. The more specific behaviors and characteristics can be found in the derived classes.

When inheriting from an existing type, you create a new type. This new type contains all the data members (even private once, although they are hidden and inaccessible) as well as duplication of the interface of the base class. In other words, objects of the derived class can receive the same messages as the original base class objects.

Let's take a look at the inheritance hierarchy shown in the following Shape example.

![Inheritance Shape hierarchy](https://www.lucidchart.com/publicSegments/view/ef12c438-282d-43e1-936e-df1fa641e8fa/image.png)

The base type here is the *Shape* class. All shapes have a size, color, position, ... All shapes can be drawn, erased, moved, colored, ... Specific shapes, such as Circle, Square and Triangle, are derived from this base class and inherit these characteristics and behavior.

Each subclass may also have additional characteristics and behavior. For example a circle has a radius while a square has the size of its side and a triangle has its width and height. Some addition behavior may be added, such as the ability to flip a Triangle (useless for a Circle and Square).

Besides that, some behavior may also be altered. For example drawing the shapes will be different for each type of Shape. This is referred to as overriding a method. When overriding a method, you keep the same interface method, but the definition (implementation) will differ from the original one.

Since all the subtypes can receive the same messages as the base type, it can be stated that the derived class is the same type as the base class. This means that we can state that:
* a Circle is a Shape
* a Square is a Shape
* a Triangle is a Shape

Because of this, inheritance is often called a **"is-a relationship"**. This can also serve as a check to see if inheritance is the correct path to follow. Type equivalence via inheritance is one of the fundamental gateways in understanding the meaning of object-oriented programming

Let's for example take a look at the following inheritance hierarchy. It may look acceptable if you state that a Bicycle is a sort of means to drive from point A to point B which you have modelled for your program. Later upon expanding your program you needed a model for a Car and noticed that it is a vehicle that can also drive from point A to point B. The only difference is that you need to keep track of mileage and allow it to be locked.

![Bad inheritance decision](https://www.lucidchart.com/publicSegments/view/1d001280-a937-4f5b-8430-dd02798ff165/image.png)

Now if you try out the same guideline and state "a Car is a Bicycle" you can definitely feel that something went wrong. While the design flaw can be spotted pretty easy here, it will not always be so obvious. A solution might be as simple as renaming Bicycle to Vehicle and if necessary create a subtype of Vehicle called Bicycle at the same level as Car.

## Abstract classes

Abstract classes are classes that cannot be instantiated, and are frequently either partially implemented, or not at all implemented. Unimplemented methods are declared but not implemented; these methods are called abstract. Abstract classes require subclasses to provide implementations for the abstract methods. If the subclass does not implement all abstract methods of the base class, it must also be defined as abstract.

Suppose we were modeling the behavior of animals, by creating a class hierachy that started with a base class called Animal. Animals are capable of doing different things like flying, digging and walking, but there are some common operations as well like eating and sleeping. Some common operations are performed by all animals, but in a different way as well. When an operation is performed in a different way, it is a good candidate for an abstract method (forcing subclasses to provide a custom implementation). Let's look at a very primitive Animal base class, which defines an abstract method for making a sound (such as a dog barking, a cow mooing, or a pig oinking).

![Animal as abstract base class](https://www.lucidchart.com/publicSegments/view/c72a0b17-c57b-477e-9060-1dc86ba25917/image.png)

Abstract classes and methods are shown in *italic* in a UML diagram.

In Java you can make a class abstract as shown below.

```java
public abstract class Animal {
   public void eat(Food food) {
      // do something with food....
   }

   public void sleep(int hours) {
      // sleep
   }

   public abstract void makeNoise();
}
```

Note that the `abstract` keyword is used to denote both an abstract method, and an abstract class. Now, any animal that wants to be instantiated (like a dog or cat) must implement the `makeNoise()` method - otherwise it is impossible to create an instance of that class. Let's look at a Dog and Cat subclass that extends the Animal class.

```java
public Dog extends Animal {
   public void makeNoise() {
     System.out.println ("Bark! Bark!");
   }
}

public Cat extends Animal {
   public void makeNoise() {
     System.out.println ("Miauw! Miauw!");
   }
}
```

Now why would you have to make the base class abstract? Could we not just given a default implementation to the `makeNoise()` method of Animal?

```java
public class Animal {
   public void eat(Food food) {
      // do something with food....
   }

   public void sleep(int hours) {
      // sleep
   }

   public void makeNoise() {
     System.out.println ("Mooooo! Mooooooo!");
   }
}
```

Or we could actually not let it do anything?

```java
public class Animal {
   public void eat(Food food) {
      // do something with food....
   }

   public void sleep(int hours) {
      // sleep
   }

   public void makeNoise() {}
}
```

Actually you don't have to make the Animal class abstract, even though there is an obvious problem with its implementation: When you are writing this program, you could type `new Animal()` and it would be valid, but it would never work as expected. As it would unexpectedly 'Mooooo' or do nothing.

Besides that a develop could inherit from Animal and forget to override the baseclass `makeNoise()` method. Than things are even worse, you may get a 'Mooooing' Dog or Cat.

Abstract classes improve the situation by preventing a developer from instantiating the base class, because a developer has marked it as having missing functionality (as being incomplete). It also provides compile-time safety so that you can ensure that any classes that extends your abstract class provides the bare minimum functionality to work, and you don't need to worry about putting stub methods (like the one above) that inheritors somehow have to magically know that they have to override a method in order to make it work.

## Interfaces

An interface lets you describe what operations can be performed on an object. You would typically use interfaces when writing methods, components, etc. that use the services of other components, objects, but you don't care what the actual type of object you are getting the services from is.

An interface is a contract: The guy writing the interface says, "hey, I accept things that take this request (method)", and the guy using the interface says "OK, the class I write can take those requests".

Consider the example of drawable objects inside a game. We create an interface called `IDrawable` that declares a method `draw(Canvas canvas)`. Every class that wants to be drawable should than implement this interface, whether it be an Animal, a Tank, a House, a Player, a Tree or a Bullet.

It is often stated that an interface is nothing more than a "Monocle" that allows you to look at objects a certain way. You only see what the interface allows you to see.

![Classes implementing the IDrawable interface](https://www.lucidchart.com/publicSegments/view/2d4ac8c6-c9b9-406e-ab49-b6c0e895f81e/image.png)

Now you may notice that this could also have been accomplished by creating an abstract super class for Tank, Tree, Player, ... But the problem is that a class can only inherit from one base class, but it can implement multiple interfaces.

This could for example be extended with a `IMakeNoise` interface as shown below.

![Classes implementing the IMakeNoise interface](https://www.lucidchart.com/publicSegments/view/70c82770-f451-4843-a7a5-9d15b33e2ba6/image.png)

Note that the Tree class makes no noise of itself and therefore does not implement the IMakeNoise interface.


Along with abstract methods, an interface may also contain constants, default methods, static methods, and nested types. Method bodies exist only for default methods and static methods.

Writing an interface is similar to writing a class. But a class describes the attributes and behaviors of an object. And an interface contains behaviors that a class implements.

Unless the class that implements the interface is abstract, all the methods of the interface need to be defined in the class.

An interface is similar to a class in the following ways:

* An interface can contain any number of methods.
* An interface is written in a file with a .java extension, with the name of the interface matching the name of the file.
* The byte code of an interface appears in a .class file.
* Interfaces appear in packages, and their corresponding bytecode file must be in a directory structure that matches the package name.

However, an interface is different from a class in several ways, including:

* You cannot instantiate an interface.
* An interface does not contain any constructors.
* All of the methods in an interface are abstract.
* An interface cannot contain instance fields. The only fields that can appear in an interface must be declared both static and final.
* An interface is not extended by a class; it is implemented by a class.
* An interface can extend multiple interfaces.

In Java interfaces have the following properties:

* An interface is implicitly abstract. You do not need to use the abstract keyword while declaring an interface.
* Each method in an interface is also implicitly abstract, so the abstract keyword is not needed.
* Methods in an interface are implicitly public.

## Combining it all

Let's combine all the knowledge we have now and try to create a bigger example.

Image a game like Pokemon where you have all different types of creatures with all kinds of abilities. For example creatures that fly and spit fire, that swim and are poisonous, that generate lightning and walk on water, ...

It is impossible to make an inheritance hierarchy based on these abilities. We could however divide them based on their animal category. Take a look at the UML diagram below.

![Pokewho The Game](https://www.lucidchart.com/publicSegments/view/f0f2b5d1-352e-434a-a525-bd2b371ba637/image.png)

[todo: explanation]

<!-- More professional example:
==> ILogable -->
