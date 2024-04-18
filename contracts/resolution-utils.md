---
order: -1
label: Resolution Utils
---

# Resolution Utils

**The easy way to resolve Avvy names**

Our Resolution Utils contract is the simplest way to interact with data on the Avvy Domains system.


## Contract Addresses

Version 		| Contract Address
---         		| ---
Proxy (Latest Version)	| [`0x5BBD3a8E215B1fC30595fd1Aba4F3FcDbB614078`](https://snowtrace.io/address/0x5BBD3a8E215B1fC30595fd1Aba4F3FcDbB614078#readContract)
V4 	 		| [`0xBf49Da93bE8879A912838B1457922A78a81D6ee3`](https://snowtrace.io/address/0xBf49Da93bE8879A912838B1457922A78a81D6ee3#readContract)
V3          		| [`0x1c7e15C29110E51D5f55d9Deb7200fbAC6665Fae`](https://snowtrace.io/address/0x1c7e15C29110E51D5f55d9Deb7200fbAC6665Fae#readContract)



## ABI

```json
[{"inputs":[{"internalType":"contract ContractRegistryInterface","name":"_contractRegistry","type":"address"}],"stateMutability":"nonpayable","type":"constructor"},{"inputs":[],"name":"contractRegistry","outputs":[{"internalType":"contract ContractRegistryInterface","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"string","name":"name","type":"string"},{"internalType":"string","name":"key","type":"string"}],"name":"resolve","outputs":[{"internalType":"string","name":"value","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"string","name":"name","type":"string"},{"internalType":"uint256","name":"key","type":"uint256"}],"name":"resolveStandard","outputs":[{"internalType":"string","name":"value","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"addy","type":"address"}],"name":"reverseResolveEVMToName","outputs":[{"internalType":"string","name":"preimage","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"string","name":"value","type":"string"},{"internalType":"uint256","name":"key","type":"uint256"}],"name":"reverseResolveToName","outputs":[{"internalType":"string","name":"preimage","type":"string"}],"stateMutability":"view","type":"function"}]
```


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

