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

A class that has atleast one abstract method is known as abtract class and you cannot create an object for the abstract class. The same 
class can be written as - 

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

