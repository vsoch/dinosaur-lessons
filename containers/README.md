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
   - The linux container API
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
 - Container providers
   - Parallels (Odin)
   - Docker (?)

## Container Basics

### What problems do containers solve?

> But it ran on my computer!

We have differences in environments, hardware, and even security, and this makes sharing of applications challenging, leading to the commonality of the phrase above.

 - Portability
 - Development Environments
   - You can spin up an entire set of components for a specific development environment, and then bring up another isolated one all at once! Containers are a dream for different kinds of developers.
 - Continuous Integration
  - The same is true for testing, You can easily test across operating systems without leaving a single host.
 - Ephemeral
   - Don't run things when you don't need to
   - Don't get locked in to one cloud vendor

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

For memory, a hypervisor can only see pages. It doesn't know what each guest is doing. WIth a container, under a single kernel the single kernel can see all objects and usage inside each container to make resource decisions. For this reason the resource decisions are made much more efficient.

### What is a virtual machine?

A virtual machine runs on a hypervisor, which is (definition). With a virtual machine, you have a virtual hardware layer, an 
entire operating system, and then libraries and applications on top of it. We can size the VM however we need - meaning it could take up.

### Virtual Machine vs Containers
Draw comparison between virtual machines

Good diagram [here](https://www.youtube.com/watch?v=YsYzMPptB-k) at 13:53 to show VM vs. container. A hypervisor image is typically
gigabytes, a container can be in the order of megabytes. When we talk about containers we talk about lightness. What are the limitations of VMs?

 - Each requires CPU, storage, memory, and an entire OS
 - More VMs == more resources
 - Portability not guaranteed

[comparison vms and containers slide 22](https://www.slideshare.net/Docker/introduction-to-docker-2017)

### Host vs. Container

Let's say we are running an application on a host. This means that we have one application on one physical server. This means:

 - slower deployment
 - more expensive, $ and resources
 - hard to migrate
 - hard to scale
 - "locked in" to a vendor because to set up somewhere else, you have to recreate the entire thing.

This is because you are using software, libraries, and dependencies on the host

But with a container, all of that flips:

 - quick deployment
 - less expensive in terms of $ and resources 
 - easy to migrate and scale
 - not locked in

The container is totally isolated - it brings all its dependencies in an environment
isolated from the operating system. [picture here](https://www.slideshare.net/Docker/introduction-to-docker-2017) on slide 18.

### Linux Container API
So if containers are so great, why did they only "become a thing"
around 2014? It's because the linux containers API is pretty compiicated. Containers in linux are controlled by [here](https://www.youtube.com/watch?v=YsYzMPptB-k) picture at 18:10:

Let's call this the kernel API, there are two things (picture at 24:45)

 - cgroups: controls resources within the kernel (io, cpu, devices, memory, network). There is something called a "freezer" that you put a bunch of processes into and put them to sleep without worrying about resources between them.
 - namespaces: pure isolation layer inside kernel. Most of time resources only belong to a single one (networking devices go in networking namespaces, ipc namespace for messages between containers, mount namespace for filesystem tree, either create a separate filesystem or use linux bind mounts to mount a piece of the host, pid namespace - init in linux needs to be running as pid 1 it isolates the process tree between containers, UTS namespace because each container needs a separate hostname, User namespace is important for "pretending to be root" without being root.)

In early containers, you could break from a container and become root on the host.

These core components are the same for all systems! They are unfortuntately very complex.

A fun history fact - these two things were developed by different open source groups. This came from an agreement at a conference in 2011 called the Kernel Summit, literally a bunch of people sitting in a room that had both developed technologies they wanted added to the linux kernel, and had to go through component by component and argue their case for their thing. At the end we did get a single cohesive thing, but it had these very two different cgroups and namespaces. 

**Important**
everything that claims to be a container technology is basically orchestrating this cgroup and namespace system. That's it. 

**Where are the namespaces?**

Here :)

```
$ ls -l /proc/self/ns/
total 0
lrwxrwxrwx 1 vanessa vanessa 0 Sep 11 12:42 cgroup -> cgroup:[4026531835]
lrwxrwxrwx 1 vanessa vanessa 0 Sep 11 12:42 ipc -> ipc:[4026531839]
lrwxrwxrwx 1 vanessa vanessa 0 Sep 11 12:42 mnt -> mnt:[4026531840]
lrwxrwxrwx 1 vanessa vanessa 0 Sep 11 12:42 net -> net:[4026532009]
lrwxrwxrwx 1 vanessa vanessa 0 Sep 11 12:42 pid -> pid:[4026531836]
lrwxrwxrwx 1 vanessa vanessa 0 Sep 11 12:42 pid_for_children -> pid:[4026531836]
lrwxrwxrwx 1 vanessa vanessa 0 Sep 11 12:42 user -> user:[4026531837]
lrwxrwxrwx 1 vanessa vanessa 0 Sep 11 12:42 uts -> uts:[4026531838]
```

**Where are the cgroups?**

Here! Each cgroup is separately mountable. 

```bash
ls -l /sys/fs/cgroup
total 0
dr-xr-xr-x 6 root root  0 Aug 29 15:00 blkio
lrwxrwxrwx 1 root root 11 Aug 29 15:00 cpu -> cpu,cpuacct
lrwxrwxrwx 1 root root 11 Aug 29 15:00 cpuacct -> cpu,cpuacct
dr-xr-xr-x 6 root root  0 Aug 29 15:00 cpu,cpuacct
dr-xr-xr-x 3 root root  0 Aug 29 15:00 cpuset
dr-xr-xr-x 6 root root  0 Aug 29 15:00 devices
dr-xr-xr-x 3 root root  0 Aug 29 15:00 freezer
dr-xr-xr-x 3 root root  0 Aug 29 15:00 hugetlb
dr-xr-xr-x 6 root root  0 Aug 29 15:00 memory
lrwxrwxrwx 1 root root 16 Aug 29 15:00 net_cls -> net_cls,net_prio
dr-xr-xr-x 3 root root  0 Aug 29 15:00 net_cls,net_prio
lrwxrwxrwx 1 root root 16 Aug 29 15:00 net_prio -> net_cls,net_prio
dr-xr-xr-x 3 root root  0 Aug 29 15:00 perf_event
dr-xr-xr-x 6 root root  0 Aug 29 15:00 pids
dr-xr-xr-x 2 root root  0 Aug 29 15:00 rdma
dr-xr-xr-x 6 root root  0 Aug 29 15:00 systemd
```

Each of these is a folder, and the
simplest one is "freezer." The way we control cgroups is via file system calls.
So, to make a cgroup called "test" I create a directory called test.
To move a process as a task into a cgroup, I can echo it there.

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
Because of these stateless workloads, we can talk about scheduling and clustering. Containers give us instant vertical scaling (up or down).

> I want elasticity

If you add a virtual machine, you need to allocate the entire set of resources in terms of memory and storage to the VM. With containers, you get elasticity. Since there is one kernel, adding a container doesn't need to create an entirely new resource because you are leveraging the resources from the host. When you put it under resource pressure, the kernel is optimized to deal with resource pressure. You can put on a physical system 3 times as many systems as you can a host provider (very useful for service providers!)

## Container Providers
Most people in the room that know about containers would readily
say "Docker" when talking about "who did this first?" but actually
it was a company called Parallels (now Odin) that organized the original meetings and container interests to lead to this common,
upstream API. But it was Docker that harnassed it to run on 
upstream containers. So they commonly get all the credit (and nobody has heard of Parallels, myself included).

Resources:

 - [VMWare: Ben Corrie Sr. Staff Engineer](https://www.vmware.com/solutions/cloud-native-apps.html)
 - [RedHat: Control Groups](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/resource_management_guide/ch01)
 - [Beginners Guide to Containers Technology](https://www.youtube.com/watch?v=YsYzMPptB-k)
