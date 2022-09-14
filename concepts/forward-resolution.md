---
order: -3
---

# Forward Resolution

Forward Resolution includes the use of two contracts:

- The `ResolverRegistry` tracks which `Resolver` should be used to resolve values for a given name. Users can define custom Resolvers or use pre-built ones.
- The `Resolver` responds to the actual query for the value.


!!!
We recommend using our client SDKs to perform forward resolution.
!!!

==- What algorithm should clients follow when performing forward resolution?

Clients perform forward resolution as follows:

1. Calculate the hash of the name
2. Call the `get(uint256 name, uint256 hash)` method on the `ResolverRegistry` to retrieve the address of the Resolver
3. Call the `resolve(uint256 datasetId, uint256 hash, string memory key)` or the `resolveStandard(uint256 datasetId, uint256 hash, uint256 key)` method on the `Resolver` (identified by the address returned in step 2) to retrieve the final value.


