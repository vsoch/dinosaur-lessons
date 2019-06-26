Once upon a time, there was a little hammer that could. She was surrounded
by others in the university cup that were in training to be scholars.
And my oh my she would watch them go! They would have the most interesting,
the most compelling burning questions about the world. And then they would summon
up a protocol to use the most fundamental tools of science and statistics to
answer it. These students were sharp. But for the little hammer that could,
she was only left to feel lacking. To her, everything looked like a nail. 
She didn't dream of finding answers, but rather building the databases 
and software that she imagined in her head. She was not scholarly, or 
sharp, she was consistent, hard working, organized,
and detail oriented. While the scholarly pupils would go off to become
academics or accreited data scientists, there was no path for her. 
But it was ironic, because the things that she cared about were so badly
needed for research practices to be reproducible, and for software
to be sustained. If she made it through her field of study at all, what would become of her? 

This is the story of the research software engineer. While it's not the typical
story for every research software engineer, it highlights the fact that
a career track historically was not well established for someone 
that wanted to work on research software, data engineering, or other
engineering practices supporting research, but didn't necessarily want to be a traditional
researcher. This is the plot that unfolds in our story today.

## A Little Background

Research is becoming increasingly more about having skills and expertise
that go well beyond a particular domain of knowledge. To be a research scientist
in this day and age, not only do you need this domain expertise, but you
also need to know some statistics, you need to be academic enough to know
how to ask and answer scientific questions, and you also need some kind of
dataset or method to do so. But expertise and data is not enough. With the increasing
demand for using computational resources and scientific programming,
practices from software engineering have become standard practice in research today.

But isn't it a little much to ask a researcher to do it all? 

In 2012 in the UK, the term "Research Software Engineering" (RSE) started to be use to
describe this specific application of software engineering to research.
In 2014 a Research Software Engineer association was created, also in the UK,
with a focus around reusability, and reproducibility of research software.
Not surprisingly, this was also around the same time as the reproducibility crisis
came about in Psychology.

Since that time, there have been similar groups established in many other countries -
Australia, Canada, Nordic Countries, New Zealand, and finally the United States. 
But here's the thing - even without this official organization, 
research software engineering has been around for a long time.
It's really that now we're finally fighting to make the profession a career
track proper. So this is our topic for discussion today. We're going to
start by defining what is an RSE, or research software engineer. We're then
going to describe a few subtypes, and then give suggestions for how you can
grow a community of RSEs at your institution.

# What is an RSE?

RSE stands for "Resarch Software Engineer," and it broadly refers to
a software engineer that specializes in research software. This spans a wide
gamut. Some RSEs are more researchers that do programming, and others are 
trained software engineers that work on research problems. If you identify
as an RSE, regardless of where you fall on this spectrum, you are likely
bringing practices from software development like version control, continuous
integration, and data provenance into workflows to support sustainable software
for research.

## Where do I find RSEs?

So where do we find these RSEs anyway? The answer is that you might need to go
looking for them. RSEs are like marshmallows hiding in a box of gold mined Lucky Charms. 
They are like mushrooms in the forest. You might not see them unless you
proactively go out looking. But maybe you are lucky, and
your institution has an official group of RSEs with a manager and campus
presence. In that case, you don't have to look very far. 
But even if your institution doesn't have any kind of official 
RSE community, you will still find RSEs scattered
about the research community. Who are they? They are lab research associates, 
postdocs, staff, and sometimes even graduate students. They can be found at universities, academic institutions,
national labs, and even companies. Sometimes larger labs can afford to hire staff to exclusively
work on tools, and research computing groups play a role in helping their users
to write code.

## What are the types of RSEs?

As mentioned previously, an RSE can range from a researcher that does a lot of
programming, to a software engineer that works in research. While no single RSE
is likely to fall within one subtype, one RSE is likely to have one or more
facets, discussed next.

### Research Software Manager

An RSE Manager is typically the lead of a group of RSEs, with a role that might
be similar to a product manager in a company, or the head of a lab. This individual
usually has expertise in software development, and is a leader not just for the
work of the group, but the individuals in it.

### Domain Developer

It's likely that many RSEs sitting within labs started with or developed
domain knowledge. For example, a researcher developing software for neuroimaging
analysis is likely to be familiar with data formats and software for brain mapping.
The domain developer might sit in a specific department or lab, and work
exclusively on developing and maintaining software for the domain. Usually input,
goals, and feedback would come from the group that the developer serves.

### Researcher

A part of being an RSE might include conducting actual research. It could be
with respect to a domain of science, but it also might be research about
software engineering, open source development, or general practices of
conducting research to begin with.


### Generalist Programmer

In stark contrast, a generalist might assist researchers
with good software development practices without having expertise about
a specific domain. For example, a statistical programmer might hold office hours
and assist researchers from departments across a university. This role can
be viewed as a service, where the programmer has expertise in his or
her practice, and researchers come to him or her to get support.

### Open Source Developer

While a generalist programmer helps researchers with code they are writing, an open source
RSE moves up one level to work on open source software that is valuable for their
user base. The open source RSE must independently seek out or use some other
method to derive what software is valued by their users, and what improvements
are needed.

### Generalist Developer

The RSE developer is by far the most challenging subtype of RSE, as it can be
more disconnected from the user base, and sometimes requires intuition about
what doesn't exist (but might) to improve research sustainability across
groups. A generalist developer does not provide a service for researchers like
the generalist programmer, but instead works on general software that
intuitively could directly or indirectly help researchers.
For example, developing new software that targets metadata provenance or
creation of reproducible containers might not tied to an existing open source
project, and is less likely to be written into a grant and requested by a lab.
However, it would likely benefit researchers across domains, and they won't know
it until the software is available to them.

For all of the above, the margins are not set in stone. For example, this 
author considers herself an open source generalist developer, primarily working
on existing and developing new open source software for research. For more RSE 
stories, see the [stories](stories) folder. Please add your story if you are
an RSE.


## What's the issue?

So what's the issue then? It's funding, of course. IT tends to vary by institution,
but one thing we can agree upon is that expertise with software engineering
is essential for reproducible research. So what does that mean? It either means
we need researchers to have prowess not only in their field of specialty, but also
as software engineers, or we need to provide some kind of research software engineering
as a service for members of an institution. The problem is that historically,
the awareness isn't there. Various groups that might hire software engineers
perhaps need to recover their salaries from grants, funding from other principle
investigators, or other monetary sources in a lab. At most institutions in the
United States, the responsibility of realizing the need for this expertise, 
hiring, and then sustaining a position has been the burden of individual labs
and small groups. Aside from groups like research computing support,
libraries, and other small institution-level groups, most institutions largely
have no floating layer of research software engineers, where, for example,
a graduate student that wanted help with development of an open source library could
go. And as a result, this hypothetical graduate student is forced to learn on his
or her own, and perhaps with the help of a postdoc in the lab. The results of this
missing layer are dire. We don't have established standards for ensuring that
the software, methods, and data that supports a publication is reproducible. We
cannot ensure that code will be maintained. Further, anyone that is interested
in these areas of work must roll their own solution for finding and funding a
position. Okay, so let's say that we do that. Is there a career track, or 
promise for future growth of the profession? Is there a community within the
instutiion to which the RSE feels a sense of belonging? The answer is no.
And frankly, this isn't good enough. It's time to foster awareness around
the importance of the RSE, and provide support and funding for them
on the level of the institution.

## Create a Community Portal

There isn't a one size fits all solution for any community, but here I'd like to make some
suggestions. If your institution doesn't have an RSE group, then you should
first start by joining communication channels of the country wide group.
For example, both the US and UK RSE groups have a Slack, email lists, and Twitter
handles. Just by getting involved, this alone can help you to feel less
along in your craft, and to start to foster relationships with other RSEs.
They might have a GitHub organization that you can join and then work on
developing a portal or group page for your specific community.

In the case that your institution has an established way to create groups of like minded
individuals, you can take advantage of that to find other RSEs that are also
hiding amongst the labs. For example, at my institution, we have something 
called "Communities of Practice."  This meant that it was was possible for me
to create a definition for the group, and link to the larger community resources.


## Communicating your Cause

Finally, you need to find other RSEs at your institution, and further, communicate your vision and
initiative. I'm not going to lie, this is really hard. While I don't have a sure fire solution,
I'd suggest that communication is going to take you far. Specifically, you might reach out to
others, and do the following:

 1. Create your community page prior to contacting anyone so that you can link them to it. You want to have a presence.
 2. Just because the idea of an RSE is familiar to you doesn't mean that everyone knows what it is. I can assure you that there are folks out there working as research software engineers that have never thought of themselves in that light. So you want to describe briefly what an RSE is, and link to documents that might better define the term.  (e.g., [this one](https://rse.ac.uk/))
 3. For your early contacts, reach out to people and groups that you know. It's easier to be forward and mention that you are just starting the initiative, and are hoping they might participate. 
 4. Tell them what it means to participate, and that they can engage to whatever degree they are comfortable with, including but not limited to:
    - a. Joining a GitHub organization and/or the community repository
    - b. Participating in discussion on a slack channel
    - c. Adding their profile to a community repository with details about support they offer to researchers
    - d. Taking on additional projects that they might think of, and be excited about.
    - e. More extended interaction with the RSE community at community events, calls, etc.
 5. It's also advisable to state your goals, as they might be meaningful for them as well. These might be any or all of the following
    - a. to better establish community for RSEs
    - b. to establish presence that is evidence that there should be more financial support for RSEs at the institution.
    - c. to better connect users with support and services they need for reproducible science 
 6. Finally, ask for their thoughts and feedback. They might have a great idea for a contribution, a new project, or an initiative for your particular community.

## Going Above and Beyond

If your community has several different groups with RSEs, it might be enough to create
unity across groups with the steps above. However, if you want to go above and beyond and
possibly work together, you could consider the following:

 - create a shared GitHub organization to work on code together
 - create a group Twitter for your community
 - have weekly, biweekly, or monthly phone or video calls to discuss collaborations

This scenario is likely more suited to smaller institutions where individuals would
benefit from working together, as opposed to RSEs sitting in separate departments with
already established projects and teams.

Can you imagine a future, where the little hammer that could, would have realized her
love for software engineering, and her desire to work in research, and then have
a clear career track and future presented to her? This is the future that we need to 
work toward. Not just for reproducible science, but for the hearts and minds of all the
little hammers, nails, and other builders out there that have yet to grow.
