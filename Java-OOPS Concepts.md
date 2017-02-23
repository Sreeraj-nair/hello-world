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

Refer to http://docs.oracle.com/javase/tutorial/java/IandI/abstract.html 

       
