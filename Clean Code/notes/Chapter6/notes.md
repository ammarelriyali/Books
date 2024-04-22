# Objects and Data Structures

#### There is a reason that we keep our variables private. We don’t want anyone else to depend on them. We want to keep the freedom to change their type or implementation on a whim or an impulse.

## Data Abstraction
##### Hiding implementation is not just a matter of putting a layer of functions between the variables. Hiding implementation is about abstractions! A class does not simply push its variables out through getters and setters. Rather it exposes abstract interfaces that allow its users to manipulate the essence of the data, without having to know its implementation.

### Don't do this
``` java 
public class Point { 
    public double x;
    public double y;
}
```
###  Do that way
 ```java
public interface Point { //interface to add layer of Abstraction
    double getX();
    double getY();
    void setCartesian(double x, double y); // setCartesian not setX or setY
    double getR();
    double getTheta();
    void setPolar(double r, double theta); 
}
 ```
 
### Don't do this
``` java 
public interface Vehicle {
    double getFuelTankCapacityInGallons(); //expose implemention 
    double getGallonsOfGasoline();  //expose implemention
}
```
###  Do that way
 ```java
public interface Vehicle {
   double getPercentFuelRemaining(); // hidden and more abstract
}
 ```
 
 ## Data/Object Anti-Symmetry
 |       | Class (oo) |  Structure (Procedural code)|
| :---        |    :----:   |          :---: |
| property      | private       | public |
| method   | have method        | only in Active Record |
| easy to add ..| data type  |  fuction |

##  Structure code be like : 
``` java
public class Square {  // square is  structure because all variable public and he doesn't hava any method
    public Point topLeft;
    public double side;
}

public class Rectangle { 
    public Point topLeft;
    public double height;
    public double width;
}

public class Circle { 
    public Point center;
    public double radius;
}

public class Geometry {
    public final double PI = 3.141592653589793;
    public double area(Object shape) throws NoSuchShapeException { // you can add mroe method easy in one class 
        if (shape instanceof Square) { 
            Square s = (Square)shape;
            return s.side * s.side;
        }
        else if (shape instanceof Rectangle) {
            Rectangle r = (Rectangle)shape;
            return r.height * r.width;
        }
        else if (shape instanceof Circle) {
            Circle c = (Circle)shape;
            return PI * c.radius * c.radius; 
        }
        throw new NoSuchShapeException(); 
    }
}
```
## Class code be like : 
```java 
public class Square implements Shape { //  Square is class because proprity is private and you polymoricm to handle fuctions 
    private Point topLeft;
    private double side;
    public double area() { // it is difficalt to add new fuction to class because you add fuction to every class availbe
        return side*side;
    } 
}
public class Rectangle implements Shape {  
    private Point topLeft;
    private double height;
    private double width;
    public double area() { 
        return height * width;
    }
}
public class Circle implements Shape { 
    private Point center;
    private double radius;
    public final double PI = 3.141592653589793;
    public double area() {
        return PI * radius * radius;
    }
}
```
`Procedural code makes it hard to add new data structures because all the functions must change. OO code makes it hard to add new functions because all the classes must change.
`
#### So, the things that are hard for OO are easy for procedures, and the things that are hard for procedures are easy for OO!

## The Law of Demeter
a module should not know about the innards of the objects it manipulates. The Law of Demeter says that a method f of a class C should only call the methods of these:
- C
- An object created by f
- An object passed as an argument to f
- An object held in an instance variable of C
- 
The method should not invoke methods on objects that are returned by any of the allowed functions. In other words, talk to friends, not to strangers.

``` java 
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
//  method getScratchDir calling from return type same as  getAbsolutePath
that expose the encapslote 
```
##### This kind of code called `Train Wrecks`
We can solve that by depend on if we you class or structure 
if structure you should use variable 
``` java 
final String outputDir = ctxt.options.scratchDir.absolutePath;
```
if clas you should use encapsltion 
``` java 
ctxt.getAbsolutePathOfScratchDirectoryOption();
```
or 
```java 
ctx.getScratchDirectoryOption().getAbsolutePath()
```
or 
``` java 
BufferedOutputStream bos = ctxt.createScratchFileStream(classFileName);
```

## Hybrids (structure and class)
Such hybrids make it hard to add new functions but also make it hard to add new data structures. They are the worst of both worlds. Avoid creating them. They are indicative of a muddled design whose authors are unsure of worse, ignorant of  they need protection from functions or types.

## Data Transfer Objects
Use when communicating with databases or parsing messages from sockets, and so on. all function in DTO is for getter and setter

## Active Record 
Like DTO but with function deal with database like save find 
`
Unfortunately we often find that developers try to treat these data structures as though they were objects by putting business rule methods in them. This is awkward because it creates a hybrid between a data structure and an object.
The solution, of course, is to treat the Active Record as a data structure and to create separate objects that contain the business rules and that hide their internal data (which are probably just instances of the Active Record).`


## Conclusion
- Objects expose behavior and hide data. This makes it easy to add new kinds of objects without changing existing behaviors. It also makes it hard to add new behaviors to existing objects. Data structures expose data and have no significant behavior. This makes it easy to add new behaviors to existing data structures but makes it hard to add new data structures to existing functions.
- In any given system we will sometimes want the flexibility to add new data types, and so we prefer objects for that part of the system. Other times we will want the flexibility to add new behaviors, and so in that part of the system we prefer data types and procedures. Good software developers understand these issues without prejudice and choose the approach that is best for the job at hand.

