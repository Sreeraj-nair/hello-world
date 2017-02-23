# Java Concepts 

## 1. What is an abstract class? 
An abstract class is a class that is declared abstract - it may or may not include abstract methods. Abstract classes cannot be instantiated (which means object to an abstract class can't be created), but they can be subclassed. 

An abstract method is a method that is declared without an implementation (without braces and followed by a semicolon), like this: 

       abstract void userLogin(String username, String password); 

If a class includes abstract methods, then the class itself must be declared abstract, as in: 

       public abstract class UserAuthentication(){
       
              //declare fields 
              // declare non abstract methods
              abstract void userLogin();
       }

When an abstract class is subclassed, the subclass usually provides implementations for all of the abstract methods in its parent class. However, if it does not, then the subclass must also be declared abstract. 

##Note: Methods in an interface (see the Interfaces section) that are not declared as default or static are implicitly abstract, so the abstract modifier is not used with interface methods. (It can be used, but it is unnecessary.)

Refer to http://docs.oracle.com/javase/tutorial/java/IandI/abstract.html 

       
