---
title: "Grab Reliability"
permalink: blog/Grab-Reliability.html
layout: post
fuzzydate: January 2013
---
Code reliability often means burning the midnight oil for a engineer who is
programming for serious real life problem. Here the serious problem I mean is the 
software that use in daily which affect the mass. Imagining the doctor could not
finish his opertion on a remote surgery, just because the network router producting by 
your company ran out of service suddenly. In this case, reliability mean a person's life.
In real world, thousands of situation need this kind of reliability to work with.
Therefore the reliability is turly changllege for a software enginneer. So a more proper
expression for this term is 
[linesOfCode.forEach(turnOneHairGrey);](http://joshholt.tumblr.com/).


Don't be scary. Sometime reliability can be got from trivial effort. Here is a story 
about reliability extracted from Kaifu Lee's Book -- 
[Making A World Of Difference](http://kaifulee.diandian.com/post/2011-11-28/7231321).

> Before we flew to New York, I cautioned Sculley that our system was new and hadn’t
> been perfected. It would look really bad if Casper suddenly died on the air. Then
> Sculley asked me, “How likely would that happen?” 
>
>
> I said, “About 10%.”
>
>
> Sculley asked, “Would it be possible to lower the failure rate to 1%?”
>
>
> I thought about it for a couple of minutes, and then replied, “OK, John, I’ll give
> it a try.”
>
> 
> ...
>
>
> Later, Sculley asked me, “How did you lower the failure rate to 1%?” 
>
>
> I replied, “I brought two computers and connected them. Had the first one gone down,
> the second one would have taken its place. Because a computer’s failure rate is 10%.
> The failure rate of both is 10% X 10% =1%. So our success rate was 99%!”

In this time, the show get its reliability by adding redundancy. But it's still very
luck thing for this big advertisement. The real reliability need much more. Redundancy
is only part of it.


Below is a list of some lessons I’ve learned that are worth being told to a new engineer.
Some are subtle, and some are surprising.


A notice must be pointed out: this list is far from being well categorized. I do not expect
to write this as an academic paper.


# Code Pratise.


## Using Design Pattern
A well choosed design pattern bring software robust. For example, 
[statechart](http://www.inf.ed.ac.uk/teaching/courses/seoc/2004_2005/resources/statecharts.pdf) can
be used in the range form embedding media player to aircraft designing. I learn this from 
[sproutcore statechart](https://github.com/sproutcore/sproutcore/tree/master/frameworks/statechart).
Statechart in [sproutcore](http://www.sproutcore.com) service as a super controller that coordinates
the each subsystem. [iCloud](https://www.icloud.com/) from apple use this to control its subsystem
(mail,contacts,picture,storage,etc). But 
[the history of statechart](http://www.wisdom.weizmann.ac.il/~harel/papers/Statecharts.History.pdf)
is farther more longer than that. It came from Israel's avionics system directly, invented by a 
professor named David Harel. The software engineers in that age made they best to make Israel's plane
more robuster. [The history of statechart](http://www.wisdom.weizmann.ac.il/~harel/papers/Statecharts.History.pdf) 
told everything.


Code pratise is 
