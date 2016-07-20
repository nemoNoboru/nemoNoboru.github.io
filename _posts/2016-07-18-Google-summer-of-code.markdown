---
layout: post
title:  "Gsoc 2016 project, CapnProto RPC"
date:   2016-07-15 16:52:07
categories: Projects Google
tags: Google Projects Ruby C++
image: /images/gitkraken.png
time: "3 minutes"
excerpt_separator: <!--more-->
---

CapnProto is a extremely fast data interchange format and a capability based RPC
system. The main point is that it has no decode/encode step.  
this means that when you have your capnproto structure build you can just write the bytes to
disk or send it over rpc.


Talking about the RPC it does "time travel", that is, you can write a bunch of methods
operating on the same value and all those methods will be coerced on just one request.
That is implemented on your code via pipelines.  
<!--more-->
Refer to the [official capnproto page][capnprotoPage] to know more.  
![time travel!][ttravel]  


Ok. Enough introduction. This summer, as a 2016 Google summer of code student my project is extend
an existing ruby binding to support the CapnProto RPC part.  


But, CapnProto is all coded on C++. Also, it needs to **generate some code** based
on your schema to work...   
And add it to your **compilation** unit...


**How do you that on ruby??**


Well, it's actually **simple**. The guys that made capnproto also made what they call a
"dynamic API" that is, a way of runtime-loading your schema and using that.
Without compiling and generating anything.  
So, with some wrapping C++ dynamic api classes on ruby and with some tweaks i have
actually [made it][linkBinding].


Also, you can check what i have done on this [link][linkCommits]


On future posts i will highlight the optimizations, design decisions and problems
that i ran into.


Also, at the time writing this posts the binding is fully working and usable.
The only existing bug is that the server don't shutdown immediately after pressing control-c.
It only exits after the next request.



[ttravel]: https://capnproto.org/images/time-travel.png
[linkBinding]: https://github.com/nemoNoboru/capnp-ruby
[linkCommits]: https://github.com/nemoNoboru/capnp-ruby/commits/master?author=nemoNoboru
[capnprotoPage]: https://capnproto.org/
