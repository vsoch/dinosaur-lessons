# Introduction to Containers

A container is a portable encapsulation of an environment. It's a
way for you to package an entire operating system, libraries, and
dependencies in a package that you can move and run anywhere.
That is the quick and dirty definition, but today we are going
to delive a little more into what this actually means. We will cover:

 - Container basics
   - The problems that containers solve
 - Virtualization
   - What is a virtual machine?
   - Virtual machines vs. containers
   - Container vs. Host
 - Definition of Container
   - Let's start with your computer
   - What is a container?
   - Containers vs. Container images.
 - Using containers
   - How do I use a container on my host?
   - How are they created?
 - Why might we use containers?
   - Operational benefits
     - automation
     - portability
     - access control
   - Runtime benefits
 - Container technologies (?)
   - Docker (?)

## Container Basics

### What problems do containers solve?

 - Variable environments
**not finished**

## Virtualization
First we talk about virtualization and introduce the idea of a VM.

A hypervisor is based on emulating hardware. When we emulate
hardware, this is called virtualization, and some of you are probably familiar with the term "virtual machine."

The biggest difference between containers and hypervisors are that **hypervisor emulation is based on emulating hardware**. So we take a machine and it emulates virtual hardware, and then bring up 
another operating system on top of that hardware.

Containers are about virtualizing the subsystems of the operating system itself. We take services that the operating system provides (networking, filesystem, etc.) and provide them in a way that is virtuaizable. So I can bring up different copies of an operating system on the same kernel. We are using features of the kernel. So you can think of it like building on the level of the kernel instead of hypervisors that build one level down, and try to emulate the hardware.

 - Containers: have a **single** kernels running underneath them
 - Hypervisors: have **multiple** kernels

A cool result of this, given that you have a single kernel, if you fix or update that kernel, all the "guests" running off it also get patched.

### What is a virtual machine?

A virtual machine runs on a hypervisor, which is (definition). With a virtual machine, you have a virtual hardware layer, an 
entire operating system, and then libraries and applications on top of it. We can size the VM however we need - meaning it could take up.

### Virtual Machine vs Containers
Draw comparison between virtual machines

## Host vs. Container

Running on host, you are using software, libraries, and dependencies on the host
The container is totally isolated - it brings all its dependencies in an environment
isolated from the operating system.


## Introduction to Your Computer

Part 1: Hello, I am your computer!

Start with showing the user the makeup of a standard linux system. Draw a box to
represent a computer, explain that it is running an operating system (linux)
and show that when you run programs you create processes. Explain that it could
be what we call "bare metal" or a "VM," the virtual machine that we just talked 
about. There is a scheduler to ensure that running the processes is efficient,
and they are sharing memory efficiently, etc.

Explain the different components (operating system vs hardware and libraries) and basic
steps of what happens when I run some software or process. Explain how this looks
a lot like virtualization, resource usage-wise.

## What is a container?

Now what if I want to isolate a process? A container is nothing more than a process,  
like one of these (point to drawn above) that has isolated (draw box around process).
This gives us a basic definition for a container:

 - a container is an encapsulation of an environment:
   - has its own process namespace. But the main container on the host is still associated with one process, and when you start that process the set within the container might kick off, and when you kill it the container's processes are also killed.

What does it mean to have its own namespace? Think of a container like a little packaged
environment, one that I can actually shell into like you would a server. When I shell
inside the container I find that it has its own little process namespace.

  - has cgroups

What is a cgroup? It's a "control group" and it's exactly that - a feature of the kernel
that lets you allocate permissions for resources. So, for example, I might allocate
a particular amount of memory, or CPU time, or network bandwidth to a set of tasks,
these processes (point to processes) that are running on my computer. What else can we
do? We can monitor them, reconfigure them, and even deny them access to resources.
So these containers also have their own set of cgroups.

## What about a container image?

The words "container" and "image" are sometimes used synonymously, but are subtly two
different things. The image is a binary sitting on your filesystem of actual stuff in
some frozen state. In docker you start from a bunch of compressed archives put together,
and some other container formats have specialized compressed filesystems as images.
A really good metaphor I like to use is that the image is the filesystem / binary that
you might have sitting somewhere, and the container is the instance of that binary. Just
like a class has instances of it, an image has instances, and we call them containers.

## Using containers

### How?

Draw box to represent host, and box to represent registry, and some client in between. 
Explain that you can pull images from the registry to run on the host, 
you get software and completely different OS on the host without installing anything.

### Building Containers

If you are a researcher, your interaction with container technology is going to
look like this:

 1. write a recipe, a text file that defines a base image, and commands to execute on top of it
 2. build the recipe into an image
 3. run / exec or otherwise interact with the image to create a container (an instance of the image)

### Why, in terms of Operational Benefits?

Why would I want to do this? If you think about it, the underlying rationale for having
and using containers is summarized by a need:

> I want to do it again.

This is called **automation** and it's the bread and butter of reproducibility in
science, continuous integration (testing) of pipelines in software engineering,
and maintenance of infrastructure. Containers help us to be efficient operationally.

> I want to do it somewhere else

This is called **portability**. With a compatible linux operating system, you can
move you binary container image to a different computer and have confidence that it
will run equivalently.

> I want to distribute my software

With registries, we now see companies shipping software as containers. The registries
give us power to define who can run what images, and from where, along with **vulnerability
scanning** to look for security issues in software. We can have *signed images** that give
us confidence about where the image has come from, and what tests it has passed. This is 
broadly called **access control**

> I care about state management

Containers are cool because they make you think hard about the states of your
filesystems, meaning persistent vs. ephemeral states in applications. These
states are extremely important to think about because transitioning between them
is very error prone. Let's start with kinds of states:

 - read only executables can be built into a container. You run them when the container starts, and when the container stops they go away.
 - read/write content needed at runtime can also be written into a container, but it will again go away when you stop the container.
 - read/write content that you write into a mounted volume to the container will persist on the host after.

These three different states you may not have thought about if you were just deploying software on the host, and then when someone else tries to deploy your thing, you realize that they are missing a file that was in the third category. It's hard to realize because it's mixed with the software and files that should be ephemeral but needed to be downloaded to install on the host. These states
can be summarized as "application state"  vs. configuration state.

The more parts of an application you can get into the read only state, the easier it is to bring
down an entire application and bring it up again, without relying on any persistent content like
a specific configuration file, for which a change could break everything.

### Why, in terms of Runtime Benefits?

> I want dynamic and stateless

You can create and throw away containers incrediby easy. It gives you the ability to do horizontal scaling.
Because of these stateless workloads, we can talk about scheduling and clustering. 


Resources:

 - [VMWare: Ben Corrie Sr. Staff Engineer](https://www.vmware.com/solutions/cloud-native-apps.html)
 - [RedHat: Control Groups](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/resource_management_guide/ch01)
 - [Beginners Guide to Containers Technology](https://www.youtube.com/watch?v=YsYzMPptB-k)
