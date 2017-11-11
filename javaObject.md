# **Brief Summary of Java Object Oriented Terminology**
*Author: Su Pengyu 11/09/2017*
## ***class***
An object represents an entity in the real world that can be distinctly identified. Anything can be viewed as an object. Objects of the same type are defined using a common class. For example, all vehicles, all house or all loans can be viewed as a class of objects.

--- 
We are goona using an simple example to discuss main components in detail.
```java
    public class circle{
        private double radius;
        public Circle() {}
        public Circle(double radius) {
            this.radius = radius;
        }
        public double getArea() {
            return Math.PI * radius * radius;
        }
    }
```
---
1. Constructor  
As its literal meaning, construcor is invoked when program needs to "build" a instance of typical class. Syntactically say, everytime program needs to build an object from class, invoking a constructor of the class using the "new" operator. In other words, ***as long as "new" appeared
in the code, there must be a constructor been invoked.***   
Note: Constructors are specical kind of method, we are able to identify constructors from three features:
    - ***Constructors must have the same name as the class itself.***
     - ***Constructor do not have a return type-- not even "void"!***
     - ***Constructor are called suing the "new" operator when an object is created. Constructors play the role of initializing objects.***    
     Using these three rules, we can find there are two constructors in this example.
     ```java
        public Circle() {}
        public Circle(double radius) {
            this.radius = raduis;
        }
        /*Like regular methods, constructors can be overloaded(multiple constructors with the
        same name ut different arguments). Eg. new Circle() invode the first constructor and new
        Circle(8.0) call the second one.
    ```
    Note:
    - A class normally provides a constructor without arguments(e.g. "public Circle()")
    - A class may be declared without constructors. ***In this situation, a non-argument constructor with an empty body is declared in this class by compile automatically.***    
---
2. Datafields    
Datafields is representing the state of an object by different values. In this case, a typicle value of radius, say 5.0 for example, states that this is a circle with radius as 5.0.
```java
private double radius;
```
---
3. Methods    
The behavior of an object is defined by a set of methods. Invoding a method on an object means that you ask that object to perform a taks. In this case, if we invoke "getArea()", we are aksing this circle to compute its area.
```java
public double getArea() {
    return Math.PI * radius * radius;
}
```
---
## ***inheritance and polymorphism***
Inheritance means deriving a new class from existing classes. If we have:
```java
class c1{...}
class c2 extends c1{...}
```
We say c1 is superclass of c2 and c2 is subclass of c1.
