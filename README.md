# Notes-of-Designing-Data-Intensive-Applications-
Notes of book &lt;Designing Data-Intensive Applications>

# Chapter 1

Three concerns that are important in software systems:

<li> Reliability

The system should continue to work correctly (performing the correct function at the desired level of performance) even in face of hardware or software faults, and human error.

Fault-tolerance mechanisms should be designed to prevent faults from causing failures. A fault is usually defined as one component of the system deviating from its spec, whereas a failure is when the system as a whole stops providing the required service to the user. In such fault-tolerant systems, it can make sense to increase the rate of faults by triggering the deliberately - for example, by randomly killing individual processes without warning. <b>By deliberately inducing faults</b>, you ensure that the fault-tolerance machinery is continually exercised and tested, which can increase your confidence that faults will be handled correctly when they occur naturally. The [Netflix Chaos Monkey][https://medium.com/netflix-techblog/the-netflix-simian-army-16e57fbab116] is an example.

<li> Scalability

As the system grows (in data volume, traffic volume, or complexity), there should be resonable ways of dealing with that growth.

<li> Maintainability

The system should be easily envolved and worked on by many different people productively.
