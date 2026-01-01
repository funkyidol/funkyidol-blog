---
title: "Novices guide to Dependency Injection & Dagger2 - Part 2 - Benefits"
date: 2019-04-21
summary: "

In the second article of the 'Novices guide to DI', before we go into further d..."
draft: false
tags: ["android", "dagger", "di", "beginners"]
canonicalURL: "https://dev.to/funkyidol/novices-guide-to-dependency-injection-dagger2-part-2-benefits-3gop"
---
In the second article of the 'Novices guide to DI', before we go into further details, lets talk about the benefits. 

Why would we event want to get into the complexity of understanding DI?
What advantages do we have by changing the way we code as discussed in the previous post: [Part 1](/blog/novices-guide-to-dependency-injection--dagger2---part-1-ga5/)

I believe that knowing the advantages of learning a concept gives an extra dose of motivation to break past the mental block and step outside the comfort zone and to reach a place where the complexity fades away and things become more clear.

Lets begin:
1. *Decoupling*:
As discussed in the previous post of the series, the whole idea of DI is to segregate the place where an object is created and where it is consumed. This decoupling is what allows for all the benefits discussed below.
2. *Reusability*:
As we now have decoupled the object creation part and shifted it away from the actual code where it gets used, we can now easily reuse it without having to write the object creation code everytime it is required in multiple places. Simply consider things like error dialogs or toast messages. If we write the dialog or toast creation code once, we dont have to write it again everytime you want to use them. Just 'inject' the object and use them.
3. *Maintainability*:
Now if you explore this possibility of having all object creation code, which is written only once throughout the code base and getting re-used everywhere, how easy it would be to perform any sort of changes (for bug fixing or new features or changed functionality) in this one place and have it gets reflected everywhere automatically without having to change it again everywhere the object was being used. This reduces the number of bugs introduced due to mismatched or improper object creation.
4. *Testability*: 
Further benefits and probably the most important one, thanks to the object creation centralization and decoupled object usage is testing. Since we now have two different entities - the object creation and the other it's usage, we can now test both these entities independently giving us a more robust overall application. We can now test the object creation by feeding it to a test code which verifies whether the created object is working fine or not. At the same time, we can test the object consumption code by feeding it with test objects of various permutations and combinations and test how our code behaves under various conditions.
I will not go much into detail on how to actually perform these testes as this is a slightly advanced topic for now.
5. *Increased development speed*:
Last but the most incrementally beneficial of the advantages is the increased development speed. Sure, in the starting of a project it might feel that its taking longer to setup the whole method injection or constructor injection but as you get into the habit, it becomes much faster. And as the application size grows, the benefits of DI starts showing as the time spent of creating objects repeatedly goes away as you confidently provide the objects to classes where they are needed.

So these are some of the benefits we get when we actually jump into the world of DI. There are even further benefits to be discussed but those are more specific to using the Dagger library itself, so those I will discuss in a separate post.

In the next post we will start with looking at Dagger and how we can use it to simplify DI
