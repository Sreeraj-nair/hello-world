# Java Concepts 

## 1. What is an abstract class? 
- If you have an idea in your mind that can be called class. 
- If you have some reality objects it is called object. 

To create an object you require a class and to define what object should do we need to define methods in class. 

Eg. You are assigned a task of designing a new mobile phone with flash light on the front but you don't know how the front flash light 
should work. 
In this case you will declare a method (for frontLight()) rather than defining it (since you don't know what it should do). 

    class MobilePhone(){


        public void camera(){

        //define the method
  
        }
  
        public void backLight(){
  
        // you know what back light does 
        // so define it
  
        }
  
        //you don't know what front light will do, but you know you want front light so declare it

        abstract void frontLight(); 

    }

## A class that has atleast one abstract method is known as an abstract class and you cannot create an object for the abstract class. 

The same class can be written as - 

    abstract class MobilePhone(){
  
        public void camera(){
    
        //define the method
    
        }
  
        public void backLight(){
    
        // you know what back light does 
    
        // so define it
    
        }
  
        //you don't know what front light will do, but you know you want front light so declare it
        abstract void frontLight(); 
    
    }

You cannot develop a mobile phone that has a front light but you don't know how it works. If you really want a new mobile phone you will have to define the way the front light works. 

If you want to use the methods defined in abstract class, it is required to create a new class that extends the abstract class. If you fail to defing frontLight() in this new class, this class will also become abstract class. If you define the frontLight(), the new class becomes concreate class. 
