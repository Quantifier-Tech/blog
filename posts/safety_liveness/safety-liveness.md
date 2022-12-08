# Safety and Liveness Properties

State = an assignment of values to variables

Behavior = an infinite sequence of states

## Safety

Safety = what must not happen

If a safety property is violated, it is violated at some particular point in the behavior.

We can talk about a safety property being satisfied by a behavior, which means that it has not been violated by any step so far.

## Liveness

Liveness = what must happen

Liveness properties cannot be violated at any particular point in a behavior.

Only by examining an entire infinite behavior, can we tell that the clock has stopped ticking, or that a message is never sent.

We use temporal logic to express liveness properties.

## Temporal logic

To understand a logic, you must understand the logic's tautologies.

(Predicate logic tautologies)

Temporal tautologies
  []F => F, [][]F <=> []F, ~<>F <=> []~F, <><>F <=> <>F, [](F /\ G) <=> []F /\ []G, <>(F \/ G) <=> <>F \/ <>G,
  []F \/ []G => [](F \/ G), <>(F /\ G) => <>F /\ <>G
  []<>(F \/ G) <=> []<>F \/ []<>G, <>[](F /\ G) <=> <>[]F /\ <>[]G

A temporal formula is true of false of a behavior!

(To boost our sense of superiority, here are the formal symbols ...)

A temporal theorem is a temporal formula that is satisfied by all behaviors.
