---
layout: post
title:  "Gsoc 2016 project, Implementing a CapnProto RPC binding in ruby"
date:   2016-07-15 16:52:07
categories: Projects Google
tags: Ruby C++ RPC
image: /images/gitkraken.png
time: "5 minutes"
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


Ok. Enough introduction. **This summer, as a 2016 Google summer of code student my project was to extend
an existing ruby binding to support CapnProto RPC.**  

the existing binding was capable of manage loading a schema, processing and saving messages.
i've made a list of the changes made in order to support RPC:


- Added support to load InterfacesSchemas
- Added support to load InterfacesSchemas Methods
- Added a rough version of a RPC client
- Added support for remotePromises
- Added support for pipelining (Client side)
- Added a better interface to the RPC client (more on this on future posts)
- Release GIL, manage exceptions, fix memory leaks in RPC client
- Wrote documentation
- Added support for CallContext
- Added a rough version of a RPC server
- Release GIL, manage exceptions, fix memory leaks in RPC server
- Added better tests of RPC on pure ruby.
- Fixed setting parameters not working properly on some cases
- Added support for pipelining (Server side)
- Optimization of RPC Client: divided CapClient on EzrpcClient and DynamicCapabilityClient
- Fixed and rewritten tests and documentation  
- Fixed binding throwing exceptions at close
- Optimization of RPC server: divided CapServer on EzrpcServer and DynamicCapabilityServer
- Rewritten tests and documentation again

By github the total of lines added is ~6k.

You can see the complete lists of commits made [here][linkCommits] and the link to
the repo is [here][linkBinding].


Also, at the time writing this posts the binding is 100% working and usable.
And provides support for a level 1 CapnProto RPC.
The only existing bug is that the server don't shutdown immediately after pressing control-c.
It only exits after the next client request is made.


[ttravel]: https://capnproto.org/images/time-travel.png
[linkBinding]: https://github.com/nemoNoboru/capnp-ruby
[linkCommits]: https://github.com/nemoNoboru/capnp-ruby/commits/master?author=nemoNoboru
[capnprotoPage]: https://capnproto.org/
