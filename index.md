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

Let us look at an example: a swarm of rescue robots. Imagine that
after a natural disaster or an accident in an industrial plant, we can
deploy robots that aid the human rescue parties by, e.g., exploring
and mapping the terrain, securing dangerous structures, locating
victims and transporting them to safety, or by sealing off radioactive
or toxic substances. Clearly this has many benefits even if the robots
are not autonomous but have to be remotely controlled by humans. But
the environment in disaster areas is often not conductive to remote
control, as wires are likely to become physically damaged and wireless
reception is often poor. In addition, human experts are already under
enormous pressure, so it would be advantageous if the robot swarm
could operate autonomously. This clearly requires the robots to adapt
to a wide range of different, dynamically changing situations.

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
pure sensor systems, some way to influence their environment.  In
addition a system has to have some mechanism for answering queries
against the stored information, otherwise it might as well not bother
to store the information in the first place.  Simple query mechanisms
may do nothing but access the information stored in the system's
memory, more sophisticated mechanisms may involve complex reasoning or
simulation steps.  Since we want to treat all systems in a unified
manner we assume that the system contains a *reasoning mechanism* of
some form.  The simple query mechanism would employ a reasoning
mechanism that performs no reasoning at all, but that's OK. To make
the problem sound more grandiose and scientific I call these
components together the *awareness mechanism* of a system.

An awareness mechanism can be realized in a myriad of ways:
information can be stored in a centralized location, it can be
distributed between agents, or it may even be stored in the
environment.  As mentioned before, the reasoner may be trivial or
sophisticated.  The interface between the awareness mechanism and the
rest of the system may be formally defined, or it may be difficult to
say where the boundary of the awareness mechanism ends, as in the case
of the immune and nervous system of animals.  The book
[The Computer after Me](http://thecomputerafterme.eu/) contains a much
more in-depth discussion of these topics.

So we now know *what* *Poem* is supposed to be good for: building
awareness mechanisms, i.e., the "brains" of adaptive, autonomous
systems.  This, of course, leads immediately to the question *how*
might *Poem* support this.  Why don't we use any old programming
language to write our awareness mechanism?

The answer to this questions is twofold and the first half may be
either reassuring or off-putting, depending on whether you like
programming or not.  Firstly, when using *Poem* you still use any old
programming language to write your system.  Currently I have written
implementations of *Poem* in Lua, in Julia and in Lisp (that covers
all the mainstream languages, right?) but there is no reason why
*Poem* might not be implemented on top of C, C++, Java or any other
language (although the Lua implementation provides a very nice
solution for C/C++-based programs).  You just add a layer on top of
the language that structures your program as a tree of behaviors.
Behaviors are similar to functions with a particular simple interface:
each behavior gets the same types of arguments and returns the same
types of results.  The standardized interface serves the same purpose
that standardized containers play for shipping goods: while the
insides of your boxes may contain wildly different things the
infrastructure does not have to care about this at all.  Inside the
user-built "behavior boxes" you may perform any activity you like, in
any way you like; from the outside they all look the same.

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

Poem
----

To build self-aware robots that exhibit useful behaviors we want to
combine fixed behavior with learning and reasoning in a flexible
manner: Behaviors for which the designers have good solutions can be
specified at design time; choices where the designers are not certain
which behavior is appropriate should be learned by experimentation at
run time; designers should be able to include guesses about
appropriate behaviors into learning or reasoning processes.  And we
want to be compatible with the main idea from predictive processing
which we summarize as "predict state or behavior at a high level; pass
this prediction down to more and more detailed behaviors, and pass
error values up.

The mechanism to achieve this in *Poem* are *partial programs*,
programs in which some parts are (more or less) unspecified.  The
unspecified parts are connected to learning or reasoning engines that
are responsible for computing the *completion* of the partial program,
i.e., a program in which all unspecified decisions have been
resolved.  To take good decisions it is often necessary to plan or
to simulate the effects of certain decisions.  Therefore *Poem* allows
the *virtualization* of the program state - the program state is
decoupled from the programs's environment and effects are only applied
to the local state.  This allows the easy integration of planning and
simulations into programs.

Surely this must be very complicated?  Fortunately the answer is a
resounding "it depends".  In *Poem* partial programs are structured as
extended behavior trees (XBTs) which are very easy to understand.  So
the basic structure of programs and the effects of virtualization and
repeated execution of program parts is easy to visualize.  However,
different learning, reasoning and planning engines introduce
complexities of their own that typically cannot be hidden from the
programmer: Using reinforcement techniques requires almost no work or
deep understanding on the part of the system designers (although
tuning them to achieve good performance does); using run-time theorem
proving requires quite a bit of background in logic and automated
theorem proving to avoid running into all kinds of complexity.

(Until October 2014 the answer would have been an unqualified
"unfortunately yes": Previous versions of *Poem* used a
non-deterministic general-purpose language to specify partial
programs; this reulted in many subtle interactions between features
and surprising behaviors.)



Continuing
----------

The easiest way to start writing *Poem* programs, is with XBTs in Lua.
The [Introduction to XBTs]({{site.url}}/xbt.html) contains a general
introduction to XBTs; the [quickstart]({{site.url}}/quickstart.html)
contains a "Getting Started" guide.  Details about using XBTs can be
found in the
[API documentation for XBTs]({{site.url}}/xbt-doc/modules/xbt.html).

Acknowledgments
---------------

The development of Poem was funded by the European project IP 257414
ASCENS ("Software Engineering for **A**utonomic
**S**ervice-**C**omponent **Ens**embles").
