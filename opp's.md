# OOP's
## Class:-
A class is a blueprint or template used to create objects. <br>
It defines:
* What data the object will have (variables)
* What behavior the object can perform (methods)

Example:
```Ruby
class Car
  def start
    puts "Car is starting..."
  end
end
```

## Object:-
An object is a real instance created from a class.

If class = blueprint <br>
Object = real product created from blueprint
```Ruby
car1 = Car.new
car1.start
```

## Inheritance:-
Inheritance means one class can reuse the properties and behavior of another class. <br>
Ruby supports single inheritance and uses modules to achieve multiple inheritance-like behavior.

- Child class can override parent method.
- `super` calls the parent class method.
```Ruby
class Animal
  def speak
    "Some sound"
  end
end

class Dog < Animal
end

dog = Dog.new
puts dog.speak
```
## Polymorphism:-
Polymorphism means “One name, many forms.” <br>
In programming, it means the same method name can behave differently for different objects.

Types of Polymorphism in Ruby :-
* Method Overriding (Runtime Polymorphism)
* Duck Typing
* Operator Overloading

## Composition:- 
Composition means a class contains objects of other classes and uses their functionality.
Instead of writing everything inside one class, we delegate responsibilities to other objects.
- This means building classes using smaller reusable objects instead of extending large parent classes.
- In simple words:

Composition = "has-a relationship" <br> 
Inheritance = "is-a relationship"

Example:

Car is a Vehicle → Inheritance <br>
Car has an Engine → Composition

Dependency injection 

## Encapsulation:-
Encapsulation means wrapping data (variables) and methods (functions) together inside a class and controlling access to them.
Instead of allowing direct access to variables, we restrict access using access modifiers.


## Abstraction:-
Abstraction means hiding complex implementation details and showing only the necessary functionality to the user. <br>
The user knows what the object does, but does not know how it does it.

Example:-
Think about a Car 🚗.

You press the accelerator

The car moves forward

But you don’t know the internal engine mechanics like fuel injection, piston movement, etc.



# Interview Questions
### The 4 pillars are:
Encapsulation <br>
Abstraction <br>
Inheritance <br>
Polymorphism

