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
From the mathmatical side, superset and subset provide a good anology of superclass and subclass. In this case, we can safely say, ***c2 is a subset of c1***. Or, ***every c2 is c1 but not every c1 is c2***.
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
>Note: Constructor invoking in instantaiting class.
When we estantaite a class, say Circle, we need to call its constructor. But considering that every Circle is a Shape, so we invoke Shape's constructor first. No matter how many layers of inheritance, computer will always invode the constructor of most "super super class".
When you define the class, if you don't writting super constructor explicitly, compiler will automatically call the super() with no arguments. But these may always leads to error because there might several constructors of super class and compiler doesn't call which one. If you write it explicity, you ***have to invoke "super()" or "super(arguments list)" at fisrt line of subclass's constructor!***
>
---
### polymorphism
Polymorphism is a word from acient greek. "Poly" always means "many forms", for example polymor means lots of small molecular in chemistry. Anyway, "Polymorphism" means Subclasses of a class can define their own unique behaviors and yet share some of the same functionality of the parent class.
If it is too abstract to understand, please carefully read codes above and we are going to explain it in detail.
```java
//base on class definitation above, we write a example main function here.
public class TestPoly{
    public static void main(String[] args) {
        Shape[] s = new Shape[];
        s[0] = new Rec(1, 2, 3, 4);
        s[1] = new Circle(1, 2, 3);
        show(s);
    }
    public void show(Shape[] s) {
        for(int i = 0; i < s.length; i++)
            System.out.println(s[i]);
    }
}
```
Print out of such code will be:
```java
This is rectangle!
This is shape!
```
In this case,super class Shape has its own toString() method, so dose as subclass Rec. But not as subclass Circle. For the method show(), it only know it will print out an array of Shapes, but don't know which toString() method it will invoked exactly. s[i] may be a Circle or a Rec, so at compiling time, your program don't know those details. These toString() method are used will be determined dynamically by JVM at runtime. This capability is called **dynamic binding** or **polymorphism**. 
>Note: sequence of polymorphism
Suppose we have a bunch of class C1, C2, C3...Cn, where C1 is subclass of C2, C2 is subclass of C3, and so on. In other word, Cn is the most general class.
If object "o" is an instance of C1. If we invokes C1's method f(), JVM searches the implementation of method f() in the order of  C1, C2, C3... Cn. Once f() is founded, search stops.
Back to our example, s[0] is an instance of Rec. JVM search toString from Rec first. Obviously, Rec's toString() is founded. So 1st line will be "This is rectangle!". In next step, s[1] is an instance of Circle who doesn't have its own toString(). Then JVM will search toString() in Shape. So 2nd line will be "This is shape!"
More generally, JVM searches invoked method f() in sequence C1, C2, C3... and stops at first implemented f().
>
---
## **abstract class/method and interface**
1. abstract class
As we discussed before, classes become more specific and concrete with each new subclass. In the reverse order from subclass to superclass, classes become more general and less specific. Sometimes a suerclass is so general and abstract that it can't have any real instances. We call them **abstract** class. Going back to our example code, this time we will make a little change so that we can discuss abstract method in detail.
```java
abstract class Shape {
    private double location_x, location_y;
    Shape() { location_x = 0; location_y = 0;}
    Shape(double location_x, double location_y) {
        this.location_x = location_x;
        this.location_y = location_y;
    }
    public String toString() {
        return "This is Shape!";
    }
    public abstract double getArea();
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
    public double getArea() {
        return length * width;
    }
}
class Circle extends Shape {
    private double radius;
    Circle() {Shape(); radius = 0;}
    Circle(double location_x, double location_y, double radius) {
        super(location_x, location_y);
        this.radius = radius;
    }
    public double getArea() {
        return Math.PI * radius * radius;
    }
}
```

Please read these simple codes first!
In practical, we know every shape must have area, so we want a     Shape.getArea() method to compute. But the problem is we are not able to knowthe area of Shape until we know the specific type of Shape, e.g. Rec or Circle.
To overcome this problem, we indtroduce abstract class and abstract method in our program. 
As you can see, I decarled an abstract double getArea() method in abstract class Shape. By declaring getArea(), we convey a message that if some class want to be subclass of Shape, it must have area. But Shape doesn't know how to compute area, so Shape just declared it. Subclass will take in charge of implementing getArea(). ***There is a important side effect on introducing abstract method in. That is, we can never instantiate an abstract class by "new SomeAbstractClass".***
>Note: ***Abstract method can only appear inside a abstract class. If a subclass of an abstract superclass does not implement all the abstract methods, the subclass must be declared abstract. In other words, in a nonabstract subclass extended from an abstract class, all the abstract methods must be implemented, even if they are not used in the subclass. Also note that abstract methods are non-static.***
---
2. interface
Interface is somehow a class like concepts that contains ***only constants and abstract methods***. Different from abstract class, we inheritate an interface use keyword ***implements***. We are not going to discuss interface here since its more easy to understand it by comparing it with abstract class.
---
## ***class VS abstract class VS interface***
1. class vs abstract class

| | Variables | Constructors | Methods |
| ------| ------ | ------ | ------|
| class | No restriction | No restriction | Only non-abstract method |
| absract class | No restriction | ***only be invoked inside subclass's constructor***.<br>Cannot be instantiated using "new" operator. | No restrictions|

2. abstract class vs interface

| | Variables | Constructors | Methods |
| ------| ------ | ------ | ------|
| interface | only ***public static final*** | No constructors | Only contains ***public abstract method***. <br>ps: You can ***omit abstract*** since it is default option. |
| absract class | No restriction | ***only be invoked inside subclass's constructor***.<br>Cannot be instantiated using "new" operator. | No restrictions|

>Note: 
abstract class can  inherit--------- ***class, abstract class and interface.***
interface only inherit --------------***interface***
>
---
##  ***validity judgement***
We will show example code firstand then provide its validity.
```java
class A {
    int a;
    A(int a) { this.a = a}
}
class B extends A{
    int b
    B(int a, int b) {
        this.b = b;
        super(a);
    }
}
```
***illegal*** ---super() or super(arguments) must be invoked in ***first*** line.

```java
class A {
    int a;
    A(int a) { this.a = a}
}
abstract class B extends A{
    int b
    B(int a, int b) {
        this.b = b;
        super(a);
    }
}
```
***legal*** ---abstract class can derived from nonabstract class and even don't have abstract method

```java
class A {...}
interface B1 {...}
interface B2 {...}

class C extends A implements B1, B2 {...}
```
***legal*** ---class can inherit ***one*** class/abstract class and ***several*** interfaces

````java
interface B {
    abstract void g();
}
abstract class A implements B{
    abstract void f();
}
````
***legal*** ---inherited method don't have to implement in abstract class/interface. Of course, you can implement it.

