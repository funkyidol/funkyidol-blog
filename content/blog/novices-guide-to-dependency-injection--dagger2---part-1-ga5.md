---
title: "Novices guide to Dependency Injection & Dagger2 - Part 1 - Introduction"
date: 2019-02-18
summary: "

This guide is an attempt to convert the difficult to understand concept of Depe..."
draft: false
tags: ["android", "dagger", "beginners"]
canonicalURL: "https://dev.to/funkyidol/novices-guide-to-dependency-injection--dagger2---part-1-ga5"
---
This guide is an attempt to convert the difficult to understand concept of Dependency Injection into a language which is easier to understand and comprehend. This article draws all the wisdom from hundred's of sources I read to wrap my head around this concept and from using it in production application.

##Defining Dependency Injection (DI)##

In very simple terms, *DI is trying to segregate the dependency creation and dependency calling*. 

Let me explain.

Dependency is any class or object that is required and is not available in the current scope. It could be a platform level class like `Toast`, a 3rd party library like `Retrofit` or your own class defined somewhere else in the project. Currently, every time you require any of these 'dependencies', you try to create its object using the `new` operator. Alternatively, you may try to use some design pattern like Singleton or Factory to call upon a preexisting object of the required dependency. 
```java
class User {
   private ProfessionalDetails pDetails = new ProfessionalDetails();
   private AcademeicDetails aDetails = new AcademicDetails();
}
```

*But now let me ask you to change the way you do things a little differently*. Instead of creating or accessing your dependencies directly, how about I tell you that all the dependencies you ever require are always provided to you via the method parameters and you never have to create a new object yourself. The above code will then look something like this:
```java
class User {
   private ProfessionalDetails pDetails;
   private AcademeicDetails aDetails;
   
   /* Example of Method (Dependency)Injection */
   public void userDetails(ProfessionalDetails pDetails, AcademicDetails aDetails){
      this.pDetails = pDetails;
      this.aDetails = aDetails;    
   }
}
```

This is called **Method  (Dependency)Injection**.

As we defined DI earlier as segregating the dependency creation and calling, here, you are not worried where or how the dependency is created, you are just concerned with using them. Similarly if any dependency you require at Class level is provided to you via the class constructor like shown below, it's called **Constructor Dependency Injection**.

Now as a first step, I implore all of my readers to stay with this thinking of not creating new dependency objects and to get the dependencies via method or constructor injection. And to take things a little further, if I can ask you reduce the use of class variables in your methods and try to pass the requirements via method parameters. This is something which will be useful when we look at the larger picture of testable code but more on that later.
