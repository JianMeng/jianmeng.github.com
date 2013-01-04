---
title: "How to make code neat"
permalink: blog/How-to-make-code-neat.html
layout: post
fuzzydate: January 2012
---

Programmers meet code everyday. Some code is neat,others looks ugly. Modifing a lousy code
is a pain in heck. For example,different indention make my eyes hard to locate code. To
let code feel good for reader, one maybe need to do a lot of edition again,which in turn
deceasing your productivity.

So how to make code neat? 
========================

Here is a few advices that I learned.

Choosing a [programming style](http://en.wikipedia.org/wiki/Programming_style).
----------------------------------------------------------------------------------
Choosing the one meet your habit, and live with them as your life style. If your are in a 
team, follow your team spec.

Break down your code into piece.
-----------------------------------
It is a logic work which need carefully consideration. Make a common part of code into a 
Macro/Function/Class. The key here is reusing code. If you are in OOP language, a lot of
design pattern books will help. If you are in C domain,a best way to learn this is reading 
open source code.

Make comments.
-----------------
Comment should be made as little as possible. Because reading comment takes time, and comments
is not code,which do not execute on a machine. So a misleading can occur. Comments should be
made as a hint.
Code below came from [box2d](http://code.google.com/p/box2d/):
{% highlight c++ %}
// Extend AABB.
b2AABB b = aabb;
b2Vec2 r(b2_aabbExtension, b2_aabbExtension);
b.lowerBound = b.lowerBound - r;
b.upperBound = b.upperBound + r;
// Predict AABB displacement.
b2Vec2 d = b2_aabbMultiplier * displacement;
{% endhighlight c++ %}
Some time a super long code occur,a lot things need to be described. So a long equal sized comment
is lovly thing accompany to code.
Code below came from [box2d](http://code.google.com/p/box2d/):
{% highlight c++ %}
// Substitute:
// 
// x = a + d
// 
// a := old total impulse
// x := new total impulse
// d := incremental impulse 
//
// For the current iteration we extend the 
// formula for the incremental impulse to
// compute the new total impulse:
//
// vn = A * d + b
//    = A * (x - a) + b
//    = A * x + b - A * a
//    = A * x + b'
// b' = b - A * a;

b2VelocityConstraintPoint* cp1 = vc->points + 0;
b2VelocityConstraintPoint* cp2 = vc->points + 1;

b2Vec2 a(cp1->normalImpulse, cp2->normalImpulse);
b2Assert(a.x >= 0.0f && a.y >= 0.0f);
// ...
// too long to write down
{% endhighlight c++ %}


Let code a bit functional.
-----------------------------
I bring some idea from the functional programming language.In functional programming language,
one variable can be assigned once only. Once assigned,its value can't be changed. It make a
variable for single purpose,and easy for reading and debuging. For example, in your important 
algorithm function, a too long function occur. In this time, you can't break down your code. 
So let's look at a simply example:
{% highlight c %}
void algorithm(){
   int sum = 0;
   // do part A job here
   {
     long a = 0x00l;
     long b = 0x01l;
     // some jobs here
     // ...
   }
   // a,b can not be refered in here
   // do part B job here
   {
     long c = 0x2323l;
     long d = 0x3232l;
     // do remaining jobs
     // ...
   }
   // c,d can not be refered in here
}
{% endhighlight c %}

Part A and B are simply code block used for sepatrating function. So variables in the code block
can not be refer outside the block. It give reader less variable to memory in function scope.
Each part of code can have different work to do.

Use a version control system.
-----------------------------
Nobody can do things one time right. Do it frequently. Modify your code if something wrong. A
version control system will be a big help in here. Personally I use git. You can choose yours.
