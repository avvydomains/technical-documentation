---
order: -3
---

# Forward Resolution

Forward Resolution is the process of taking a `.avax` name and using it to retrieve a value, such as an `0x` address for EVM chains. An important property of forward resolution is that *many* `.avax` names can resolve to the same value.


### How does forward resolution work?

Forward Resolution includes the use of two contracts:

- The `ResolverRegistry` tracks which `Resolver` should be used to resolve values for a given name. Users can define custom Resolvers or use pre-built ones.
- The `Resolver` responds to the actual query for the value.


==- What algorithm should clients follow when performing forward resolution?

**Step 1. Find the address of the Resolver contract**

To find the address of a Resolver contract for a name, we hash the name then call the `get(uint256 name, uint256 hash)` method on the `ResolverRegistry`.

It is possible that there is no entry for the name in the `ResolverRegistry`. If the name has two or less labels (e.g. `myname.avax` has two labels), forward resolution fails. If the name has three or more labels, the lowest tier label should be removed & the process should be repeated (e.g. for `subdomain.domain.avax`, we should repeat the process with `domain.avax`).

**Step 2. Query the Resolver contract**

If we have found an address for a Resolver contract, we can resolve a value as follows:

- For custom records, call `resolve(uint256 datasetId, uint256 hash, string memory key)`
- For standard records, call `resolveStandard(uint256 datasetId, uint256 hash, uint256 key)`

===

!!!
We recommend using our Client Libraries to perform forward resolution.
!!!

### Security Notes

There is absolutely no sanitization or authentication performed on the *values* set for forward resolution. Registrants of a `.avax` name have full control to set values; client applications of all kinds should treat these values as untrusted.

