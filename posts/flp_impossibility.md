# FLP Impossibility

[in depth](https://www.the-paper-trail.org/post/2008-08-13-a-brief-tour-of-flp-impossibility/)

consensus
- solvable in the synchronous setting even in the presence of faults
- failure detection

In the asynchronous setting, fault detection is impossible and no distributed algorithm can exist to solve consensus when even a single processor can crash

## Consensus

- agreement
- termination - strong or weak
- validity

E.g. committing transactions to a distributed database

## System model

Set of assumptions made about the distributed system, i.e. context/environment for execution of a distributed algorithm

Great variety, but common elements
- network of distributed processes
- communication graph/topology

Differ on
- processor view of time
- communication link reliability
- whether and how processors are allowed to fail

### Asynchronous communication

- no upper bound on message processing and passing
- impossible to tell if a processor has failed or just hasn't responded yet

No consensus if links are arbitrarily unreliable so they are assumed to be reliable
- TCP provides reliable enough message delivery

### Fail-stop faults

- processors simply stop responding to all messages

### Formal model

message buffer (multiset of messages) with two operations
- `send(p, m)` - places the message `m` in the buffer for `p`
- `receive(p)` - either returns a message for `p` (and removes it from the buffer) or a special value `θ`, which does nothing, i.e. returns a message option. The only requirement is that calling `receive(p)` infinitely many times will deliver all messages in the buffer to `p`, i.e. messages may be delayed arbitrarily, but not completely lost

#### Configuration

Basically the global state of the system
- internal state of all processors
- contents of the message buffer

The system evolves in *steps* which consist of a processor `p` performing `receive(p)` and moving to another internal state. Each step is uniquely determined by the message received (possibly `θ`) and the process that received it. This pair is called an *event*.

*schedule* = sequence of events starting from a configuration C (actions)
*run* = sequence of steps taken to realize the schedule (states)

Non-faulty processes take infinitely many steps in a run (eventually just receiving `θ` once the algorithm has finished)

*Admissible* run is one in which at most one process is faulty and every message is eventually delivered

A run is called *deciding* if there exists at least one process which decides according to the rules of consensus and a consensus protocol is called *totally correct* if every admissible run is deciding

## The theorem

No totally correct consensus algorithm exists in an asynchronous system model in which even a single process fails

Proved by showing there exists an admissible run which is not deciding
- infinite loop of bivalent configurations

### Proof

Lemma 1 - proves the existence of bivalent initial configurations

Lemma 2 - proves that starting from a bivalent configuration, it is always possible reach another bivalent configuration by delaying a pending message
