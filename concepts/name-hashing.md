---
order: 0
---

# Name Hashing

Names are identified by their hash on-chain. Publishing the preimage of the hash is optional. 

A detailed explanation of the motivations behind our hashing mechanism is available in the blog post [Privacy Mechanisms for Name Registrations](https://avvy.domains/blog/privacy-mechanisms-for-registrations/).

We highly recommend using our client libraries to handle operations related to hashing.

==- How does the hashing algorithm work?

Names must be in lower case before starting this process.

We use the [Circom](https://iden3.io/circom) implementation of the Poseidon hash function, initialized with three inputs.

Given a name that consists of `n` labels, we perform `n` rounds of Poseidon where the first input is the output hash from the previous round (or `0` for the first round) and the second & third inputs are derived from the current label. We refer to the second & third inputs as `input signals`.

Each label can consist of 62 characters in the set `[a-z0-9-]`. We convert a label to input signals by splitting the label into two strings of 31 characters. Each of these strings is then converted into a 248-bit string, then into an integer. The resulting integers are the input signals for the hashing function.
===

Users are able to register their names using only the hash. This the first of a number of privacy features which allows users to utilize the system without creating visible links of information on-chain.


### What are Input Signals?

The hashing algorithm that is used to hash the domains accepts only integer inputs. Any name consisting of `n` labels can be converted to a set of `n * 2` input signals, which can then be used as inputs in our hashing algorithm.

!!!
Example: the name `myname.mydomain.avax` has 3 labels and can be converted to a set of 6 integers known as the *Input Signals*
!!!
