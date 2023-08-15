---
order: 0
icon: rocket
---

# Getting Started

The most common integration use-cases for Avvy Domains are:

- **Forward Resolution**, where we take a `.avax` name and get a value like an `0x` address. This can be useful for scenarios like improving the UX for transferring funds between wallets.
- **Reverse Resolution**, where we take a value like an `0x` address and find the associated `.avax` name. This can be useful for adding identity to applications, making it easier for users to read information.

In most cases integrators will want to use our [Resolution Utils contract](/contracts/resolution-utils/) to perform these operations. 
