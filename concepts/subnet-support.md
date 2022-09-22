---
order: -6
---

# Subnet Support

How does Avvy Domains support subnets on Avalanche? 

Let's look at each of the core offerings, `Forward Resolution` and `Reverse Resolution`, to understand how each can be adapted to support subnets (and any network).

Before continuing, please review the following documentation:

- [Records & Record Types](/concepts/record-types/)
- [Forward Resolution](/concepts/forward-resolution/)
- [Reverse Resolution](/concepts/reverse-resolution/)


### Forward & Reverse Resolution for Subnets

For subnets and alt networks we must look at the identifiers used on the network. Many subnets will be EVM-precompiles - such subnets are supported by default via the EVM/C-Chain Address record. Other subnets (e.g. those supporting [CosmWasm](https://docs.cosmwasm.com/docs/1.0/architecture/addresses/)) will have different types of identifiers.

For Forward Resolution, we simply need to establish a Standard Record Type for the type of identifier.

Reverse Resolution is more complicated as we must verify ownership of a given identifier in order to associate it with a `.avax` address. This requries a custom smart contract to verify some proof of ownership for the identifier.



### Questions & Support

If you are seeking support for a particular VM / Subnet / Network, please [touch base via our chat channels](/contact/).
