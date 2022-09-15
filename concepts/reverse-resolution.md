---
order: -4
---

# Reverse Resolution

Reverse Resolution is the process of taking a standard value, such as an `0x` address, and using it to retrieve an associated `.avax` name. 

An important property of reverse resolution is that each unique value can only resolve to a single `.avax` name.

!!!
Reverse Resolution is only supported for Standard Record Types. Custom Records are not supported.
!!!

### How does reverse resolution work?

Each type of value (e.g. EVM address, X-Chain address) requires a separate `ReverseResolver` contract. The `ReverseResolverRegistry` maintains pointers to the `ReverseResolver` contracts that should be used for each type of value.

After finding the relevant `ReverseResolver` address, that contract is used to fetch the value.

==- What algorithm should clients follow when performing reverse resolution?

**Step 1. Find the address of the ReverseResolver contract**

Given a numbered Standard Record Type (e.g. 3 for EVM), call `getResolver(uint256 standardKey)` on the `ReverseResolverRegistry`.

**Step 2. Query the ReverseResolver contract**

Call `get(target)` on the `ReverseResolver` to return the associated hash.
===

!!!
We recommend using our Client Libraries to perform reverse resolution.
!!!

### Authenticators

The `ReverseResolverRegistry` handles permissioning for setting records on Reverse Resolvers. When a user attempts to set a reverse record, the Reverse Resolver will ask the Registry whether the user has permission to do so. 

By default, the ReverseResolverRegistry will check whether the name is expired and whether the user is the current owner of the name. This default functionality can be overridden by deploying a custom authenticator contract & directing the ReverseResolverRegistry to use that custom authenticator contract for the name.

An Authenticator contract implements a single `canWrite(..)` method which returns a boolean value.
