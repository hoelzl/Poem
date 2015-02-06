---
title: Poem
subtitle: A language for designing awareness mechanisms
---

Poem is a language for designing awareness mechanisms for adaptive,
autonomous systems. What does that mean, exactly?

Autonomy, Awareness and Self-Expression
---------------------------------------

Many software-intensive systems deployed today are large and complex,
and they are often connected to the Internet which is even larger and
more complex. It is simply no longer possible to have operators
continuously monitor the components of a system, tune it to the specific
circumstances it encounters or diagnose malfunctions---these are things
systems should do on their own. Put another way, systems should be
adaptive and able to operate autonomously.

Let us look at an example: a swarm of rescue robots. Imagine that after
a natural disaster or an accident in an industrial plant, we can deploy
robots that aid the human rescue parties by, e.g., exploring and mapping
the terrain, securing dangerous structures, locating victims and
transporting them to safety, or by sealing radioactive or toxic
substances. Clearly this has many benefits even if the robots are not
autonomous but have to be remotely controlled by humans. But the
environment in disaster areas is often not conductive to remote control,
as wires are likely to become physically damaged and wireless reception
is often likely to be poor. In addition, human experts are already under
enormous pressure, so it would be advantageous if the robot swarm could
operate autonomously. This clearly requires the robots to adapt to a
wide range of different, dynamically changing situations.

The big question is, of course, how can we build these kinds of
systems?  And in particular, how can we build them to do the right
thing even when they encounter circumstances that the designers have
not foreseen, or, as is the case for the hypothetical rescue robots,
when the designers don't even know very much about the environment in
which the system will be operating. After all, the rescue robots are
not much help, if their actions endanger the victims or rescue
personnel.

There are many ways to answer this question, from mostly reactive
systems to sophisticated reasoners operating on vast knowledge bases.
And most of them are probably correct, at least for certain scenarios
and use cases.  There are, however, certain features that *all*
systems that can reasonably be called autonomous and adaptive share:
they need some way to store information, some way to receive
information from their environment and, unless we are dealing with
pure sensor systems, some way to influence their environment.  There
are many ways how these functionalities can be realized: information
can be stored in a centralized location, distributed between agents,
or even in the environment.  The interface between the awareness
mechanism may be formally defined, or it may be difficult to say where
the boundary of the awareness mechanism ends, as in the case of the
immune and nervous system of animals.  The book
[The Computer after Me](http://thecomputerafterme.eu/) contains a much
more in-depth discussion of these topics.

For most systems that we build we have a definite idea what the system
should achieve (even if we don't know how to implement a solution, or
even what a solution might look like).  Let's assume that we can, at
least in theory, write down a (possibly time dependent) utility
function that formalizes this vague idea and imbue our system with
this utility function.  We would then like our system to use its
awareness mechanism in order to improve this utility function.  If it
actually does this we call the system *self expressive*.  In many
cases it seems to be self expression, rather than awareness itself,
that seems to pose the biggest challenges for system designers.

Here, no there, no everywhere...
--------------------------------

Of course the image of helpful robotic assistants that valiantly
rescue disaster victims without human oversight is not particularly
realistic.  Even in controlled conditions robots struggle to perform
much simpler tasks as soon as they require adaptation to unforeseen
circumstances, in spite of the tremendous progress that has been made
in many areas of artificial intelligence and machine learning.

There are many reasons for this, but I want to focus on one particular
aspect: in most situation where adaptation is required there is a huge
space of possible inferences we can draw and behaviors we can
try---almost all of them irrelevant to the problem.  This is,
obviously, in no way a novel observation, and many ways to tame the
problem of state explosion have been proposed.  One of the most
interesting developments in this area is the theory of
[predictive processing](http://www.ncbi.nlm.nih.gov/pubmed/23663408)
that was proposed by neuroscientists.  The traditional model of
"intilligent" systems supposes that sensors deliver raw data to a
reasoning system that processes this data and sends the actions that
should be performed to the actuators of a system (this possibly
happens in several layers).  Predictive processing in contrast
supposes that neuronal processing happens in a multi-layer network, in
which the higher layers generate predictions of the sensor data and
pass these predictions to the lower layers.  The lower layers, in
turn, pass the error of these predictions up.


Acknowledgments
---------------

The development of Poem was funded by the European ASCENS project
("Software Engineering for **A**utonomic **S**ervice-**C**omponent
**Ens**embles").
