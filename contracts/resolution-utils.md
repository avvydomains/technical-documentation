---
order: -1
label: Resolution Utils
---

# Resolution Utils

**The easy way to resolve Avvy names**

Our Resolution Utils contract is the simplest way to interact with data on the Avvy Domains system.

The latest version, `ResolutionUtilsV2`, is deployed at [`0x1ea4e7A798557001b99D88D6b4ba7F7fc79406A9`](https://snowtrace.io/address/0x1ea4e7A798557001b99D88D6b4ba7F7fc79406A9#readContract).


## Examples

### Finding the 0x address for a domain

We use the `resolveStandard` method with the following arguments:

- `name`: `avvydomains.avax`
- `key`: `3` (EVM address)

This returns the 0x address associated with the domain, if one exists.

### Finding the domain for an 0x address

We use the `reverseResolveEVMToName` method with the following arguments:

- `addy`: (0x address)

This returns the `.avax` domain name associated with the domain.
