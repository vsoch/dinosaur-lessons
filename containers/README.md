# Introduction to Containers

Notes from:

 - VMWare: Ben Corrie Sr. Staff Engineer https://www.youtube.com/watch?v=EnJ7qX9fkcU

## History of Containers

Need to talk about virtualization and introduce the idea of a VM.

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
   - has its own process namespace

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

