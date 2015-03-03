---
title: Poem
subtitle: A language for designing awareness mechanisms
---

Poem is a language for designing awareness mechanisms for adaptive,
autonomous systems.

Wait, what does that mean, exactly?

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
try---almost all of them irrelevant to the problem.  If, for example,
you use a theorem prover to reason about desirable robot behaviors and
you have a sufficiently rich vocabulary in your logic, then you will
often observe the following phenomenon: You input a query how to
navigate from *A* to *B* to the reasoner, and it starts with reasoning
steps that seem natural enough.  But then it stumbles upon some
formula that connects locations with activities, and soon your
reasoner ponders questions such as "Will picking up a victim in
location *C* result in a higher reward than assisting robot *X*
transport a victim from *D* to *E*?"  While this question may be
interesting, it will not really help you solve your navigation problem
(and it includes another navigation problem of its own).  Instead of
staying focused on getting from here to there the reasoner goes
everywhere to find a solution.

This is, obviously, in no way a novel observation, and many ways to
tame the problem of "proof state explosion" have been proposed for
inference engines: set of support strategies that limit new inference
steps to predicates that occur in the query or in previous inference
steps; predicate ordering strategies, pruning branches in the proof
tree by rewriting, etc.

But one of the most interesting contributions to the problem of
guiding reasoning comes from the theory of
[predictive processing](http://www.ncbi.nlm.nih.gov/pubmed/23663408)
that was proposed by neuroscientists and works in a very different
manner: it changes the problem from reasoning to prediction.  The
traditional model of "intilligent" systems supposes that sensors
deliver raw data to a reasoning system that processes this data and
sends the actions that should be performed to the actuators of a
system (this possibly happens in several layers).  Predictive
processing in contrast supposes that neuronal processing happens in a
multi-layer network, in which the higher layers generate predictions
of the sensor data and pass these predictions to the lower layers.
The lower layers, in turn, pass the error of these predictions up.
Predictive processing is closely connected to an area of machine
learning called [deep learning](http://deeplearning.net/) that has
been applied very successfully to a number of hard machine learning
problems.  And in fact the Poem runtime (called *Iliad*) contains not
one but two third-party frameworks for deep learning (one written in
Lisp for easy integration with the reasoners, one in LuaJIT for easy
integration with the rest of the world).

So we're all set, right?  Just put everything into a deep learner, and
obtain an intelligent agent.

As you surely know, this is not going to work for a number of
reasons, for example:

* it's not clear how to even describe the behavior of a robot in such
  a way that you can apply learning techniques to it;

* learning everything a robot needs to do takes a lot of time;

* relying on behaviors learned autonomously leaves developers very
  little control over the system and is likely to result in many
  unwanted behaviors;

* currently available techniques work rather poorly for learning
  distributed behaviors.


Acknowledgments
---------------


The development of Poem was funded by the European project IP 257414
ASCENS ("Software Engineering for **A**utonomic
**S**ervice-**C**omponent **Ens**embles").
