---
order: -1
---

# Registration Privacy & Revealing a Name

Registrations can be made with `Standard Privacy` or `Enhanced Privacy`. At a technical level, a `Standard Privacy` registration means that a user published the preimage of their name to the chain while an `Enhanced Privacy` registration has not. That is the only difference.

We achieve this by publishing the `Input Signals` of a name to the `Rainbow Table` contract. This is known as Revealing a Name. 

!!!
Any user can publish the Input Signals for a name as long as the signals correspond to the hash provided.
!!!

### Finding the preimage of a hash

Client applications can query the `Rainbow Table` with a hash. If the preimage hash been published to the Rainbow Table it will be returned in the Input Signal format. The client application can then decode the Input Signals into the ascii name.

We recommend using the provided client libraries to handle these tasks.
