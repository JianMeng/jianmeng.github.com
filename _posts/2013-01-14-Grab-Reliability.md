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


# Coding Practices 


## Using Design Pattern
A well choosed design pattern bring software robustness. For example, 
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
told you everything.


## [Test-driven development(TTD)](http://en.wikipedia.org/wiki/Test-driven_development)
I know this from a meetup lecture giving by [Zoom.Quite](http://about.me/zoom.quiet).
The slide is in [here](http://zoomquiet.org/res/s5/100826-PyTDD/). Dynmatic language like
python is sharp on TTD. 


And one also can not miss the browser-side TDD. Javascript framework evolve fastly in recent years.
Some programmer pick up [qunitjs](http://qunitjs.com/), while other choose to develop they testbed in a
single page, for example [sproutcore testing](https://github.com/sproutcore/sproutcore/tree/master/frameworks/testing).


## [Continuous integration](http://en.wikipedia.org/wiki/Continuous_integration)
Automated unit tests is a big help for software development. With Continuous integration(CI), automated 
unit tests can be done daily. A mistake such as new code invailding other part function can be found 
faster and cheaper. Although building a CI enviroment never be easy, it turly boost the productivity of 
 programmer.


## Code Review
Code review is a tool for team to re-ensure software quality. The whole team ensure the quality of project,
not just one single person. Code review can be done by issue, by spring, by GA. A whole team choose which is
best time to do reviewing.


Another benefit bring by code review is that educating the newbie in the team. Young team member can learn
a lot skill that will be helpful in future work.


## Paired programming
Personally, I thought paired programming is a waste of human resource. Costing doubled, but product still 
same. Not a good deal!


But one experience on annoying UI bug changed me forever. That bug cause by a mis-usaging design. When my 
parter and I finally realize that reason, it is too late for me to ask designer to change. So we two had 
to continue the full-of-if-else design. It is 2 am. Both of us is tired. Writing down 200 lines of if-else 
is easy job for that time me. When one man can not got the job done, paired programming came in. Using 
this we make our work done.


## Distributed Systems

If one server is not reliable for you, you can run two server. Distributed system is considered to work
with this situation. For telecom company, distributed system is a must to their products. But distributed
system will cost much more resources than one single system. [Distributed Systems for Young Bloods](http://
www.somethingsimilar.com/2013/01/14/notes-on-distributed-systems-for-young-bloods/) is something you need 
to read.


# Math hack
Math is the key for programming. My favorite article on this is 
[The Mathematical Hacker](http://evanmiller.org/mathematical-hacker.html). The safty come form math is reliable.
Math works in Kaifu Lee's story above.

