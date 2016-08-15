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

# introduction

CapnProto is a extremely fast data interchange format and a capability based RPC
system. The main point is that it has no decode/encode step.  
This means that when you have your capnproto structure build you can just write the bytes to
disk or send it over rpc.


Talking about the RPC it does "time travel", that is, you can write a bunch of methods
operating on the same value and all those methods will be coerced on just one request.
That is implemented on your code via pipelines.  
<!--more-->
Refer to the [official capnproto page][capnprotoPage] to know more.  
![time travel!][ttravel]  

# Project

Ok. Enough introduction.  
**This summer, as a 2016 Google summer of code student my project was to extend
an existing ruby binding to support CapnProto RPC.**  

The existing binding was capable of manage loading a schema, processing and saving messages.

# Philosophy

I tried to integrate my code seamlessly with the existing binding and follow the 'style' of the original developer.  
I reuse lots of the classes that were already there and tried to code on a modular way.
And after coding a rough, monolithic RPC client i had cut it out into two or more modules following the class hierarchy of the main library,
CapnProto.

# Work done

- Added support to load InterfacesSchemas
- Added support to load InterfacesSchemas Methods
- Added a rough version of a RPC client
- Added support for remotePromises
- Added support for pipelining (Client side)
- Added a better interface to the RPC client
- Fix memory leaks in RPC client and make it release the GIL
- Wrote documentation
- Added support for CallContext
- Added a rough version of a RPC server
- Manage exceptions, fix memory leaks in RPC server and make it release the GIL
- Added better tests of RPC on pure ruby. (i was doing testing with a ruby client and a C++ server)
- Fixed setting parameters not working properly on some cases
- Added support for pipelining (Server side)
- Optimization of RPC Client: divided Client on EzrpcClient and DynamicCapabilityClient
- Fixed and rewritten tests and documentation  
- Fixed binding throwing exceptions at close
- Optimization of RPC server: divided Server on EzrpcServer and DynamicCapabilityServer
- Rewritten tests and documentation again

By github the total of lines added is ~6k.


# Status

**You can see the complete lists of commits made [here][linkCommits]** and the link to
the repo is [here][linkBinding].


I published [my gem][link_gem] to the [official Ruby community gem hosting service][rubygems] so everyone can install and use it.
All my work is on github with the issue system open.


Also, at the time writing this posts the binding is 100% working and usable.
And provides support for a level 1 CapnProto RPC.   
The gem is on a pre release, was published 3 days ago and it has already +50 downloads. With no issues at all.

# Bugs found

The only existing bug is that the server don't shutdown immediately after pressing control-c.
It only exits after the next client request is made.


[ttravel]: https://capnproto.org/images/time-travel.png
[linkBinding]: https://github.com/nemoNoboru/capnp-ruby
[linkCommits]: https://github.com/nemoNoboru/capnp-ruby/commits/master?author=nemoNoboru
[capnprotoPage]: https://capnproto.org/
[link_gem]: https://rubygems.org/gems/capn_proto-rpc
[rubygems]: https://rubygems.org/
