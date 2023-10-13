---
order: -1
label: Resolution Utils
---

# Resolution Utils

**The easy way to resolve Avvy names**

Our Resolution Utils contract is the simplest way to interact with data on the Avvy Domains system.

The latest version, `ResolutionUtilsV3`, is deployed at [`0x1c7e15C29110E51D5f55d9Deb7200fbAC6665Fae`](https://snowtrace.io/address/0x1c7e15C29110E51D5f55d9Deb7200fbAC6665Fae#readContract).


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

### Finding the domain for a Validator NodeID

We use the `reverseResolveToName` method with the following arguments:

- `value`: `NodeID-[x]`
- `key`: `4` (Validator)

This returns the `.avax` domain name associated with the validator.

