
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
>Note: Constructors are specical kind of method, we are able to identify constructors from three features:
    - ***Constructors must have the same name as the class itself.***
     - ***Constructor do not have a return type-- not even "void"!***
     - ***Constructor are called suing the "new" operator when an object is created. Constructors play the role of initializing objects.***    
     Using these three rules, we can find there are two constructors in this example.
>
     ```java
        public Circle() {}
        public Circle(double radius) {
            this.radius = raduis;
        }
        /*Like regular methods, constructors can be overloaded(multiple constructors with the
        same name ut different arguments). Eg. new Circle() invode the first constructor and new
        Circle(8.0) call the second one.
    ```
> Note:
    - A class normally provides a constructor without arguments(e.g. "public Circle()")
    - A class may be declared without constructors. ***In this situation, a non-argument constructor with an empty body is declared in this class by compile automatically.***   
>
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
### inheritance
Inheritance means deriving a new class from existing classes. If we have:
```java
class c1{...}
class c2 extends c1{...}
```
We say c1 is superclass of c2 and c2 is subclass of c1.
As the Venn Diagram listed showing, we can generally verify the relationship between superclass and subclass. 
From the mathmatical side, superset and subset provide a good anology of superclass and subclass. In this case, we can safely say, ***c2 is a subset of c1***.(***$$c2 \subseteq c1$$***)  
Or, ***every c2 is c1 but not every c1 is c2***.
---
>Understanding the collection relationship is essential in writting these kind of code:
```java
import java.util.List;
import java.util.ArrayList;
import java.util.LinkedList;

public class A {
    public static void main(String[] args) {
        List<Integer> list1 = new ArrayList<Integer>();
        List<Integer> list2 = new LinkedList<Integer>();
    }
}
```
>As a beginner in Java, we may confused by this kind of variable initialization. In order to analyze this code, we may cut it from "=" as left part and right part. 
In the left part"List<Integer> List1", we decalared a new viriable "firstList" in List type. This part means, I need a new list to store integers and name it as "list1". I don't care what kind of list it is, as long as it is a list.
In the right part"new ArrayList<Integer>();", we actually "create" an ArrayList<Integer> and assign it to list1. Since in the left part, we only care about if list1 is a list, so we can eigher assign an ArrayList or a LinkedList to that variable.
When using this kind of syntax, remember to ask yourself"Is every List an ArrayList? Or Is every ArrayList a List? " Also, we are actually considering the relationship between superclass and subclass. In this case, List is superclass and ArrayList/LinkedList is subclass. CORRECT!
---
In pactice, we use superclass representing those general concepts like Vehicle and use subclass representing specific concepts like Bus. We should always remember that ***superclass should be general and subclass should be specific.***
![---Venn Diagram---](https://github.com/banziFD/Document/blob/master/image/super_sub_class.jpg)
> Terminology Review
superclass = supertype = parent class = base class
subclass = subtype = child class = extended class = derived class
>

As what we have done before, we enlarge our example code to help our discuss.
```java
class Shape {
    private double location_x, location_y;
    Shape() { location_x = 0; location_y = 0;}
    Shape(double location_x, double location_y) {
        this.location_x = location_x;
        this.location_y = location_y;
    }
    public String toString() {
        return "This is Shape!";
    }
}
class Rec extends Shape {
    private double  length, width;
    Rec() {Shape(); length = 0; width = 0;}
    Rec(double location_x, double location_y, 
    double length, double width) {
        Shape(location_x, location_y);
        this.length = length;
        this.width = width;
    }
    public String toString() {
        return "This is rectangle!";
    }
}
class Circle extends Shape {
    private double radius;
    Circle() {Shape(); radius = 0;}
    Circle(double location_x, double location_y, double radius) {
        super(location_x, location_y);
        this.radius = radius;
    }
}
```
>Note: Constructor invoking in estantaiting class.
When we estantaite a class, say Circle, we need to call its constructor. But considering that every Circle is a Shape, so we invoke Shape's constructor first. No matter how many layers of inheritance, computer will always invode the constructor of most "super super class".
When you define the class, if you don't writting super constructor explicitly, compiler will automatically call the super() with no arguments. But these may always leads to error because there might several constructors of super class and compiler doesn't call which one. If you write it explicity, you ***have to invoke "super()" or "super(arguments list)" at fisrt line of subclass's constructor!***
>
---
### polymorphism
Polymorphism is a word from acient greek. "Poly" always means many, for example polymor means lots of small molecular in chemistry. Anyway, "Polymorphism" means Subclasses of a class can define their own unique behaviors and yet share some of the same functionality of the parent class.
If it is too abstract to understan, we show it in codes.








