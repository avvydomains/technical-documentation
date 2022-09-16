---
order: -1
label: Events & Indexing
---

# Events & Indexing

Indexers of the project may need to watch event logs to recompile the state of the Avvy Domains system offline.

!!!
We recommend using our Indexer tool to compile an offline index of the Avvy Domains system.
!!!


### Domain Events

The `Domain` contract emits a number of events relating to registrations.

```solidity
// The Register event is emitted when a domain is registered or renewed
event Register(
	address agent, // the address of the contract which made the registration
	address indexed registrant, // the registrant of the domain
	uint256 indexed name, // the hash / tokenId of the domain that was registered
	uint256 leaseLength // the registration expires at `block.timestamp + leaseLength`
)

// The Recycle event is emitted when an expired domain is claimed at auction
event Recycle(
	address agent, // the address of the contract which made the registration
	address indexed registrant, // the registrant of the domain
	uint256 indexed name, // the hash / tokenId of the domain that was registered
	uint256 leaseLength // the registration expires at `block.timestamp + leaseLength`
)

// The Transfer event is from OpenZeppelin's ERC721
event Transfer(
	address from,
	address to,
	address tokenId // this will be the hash of the domain
)
```

Avvy Domains also supports two sensitive operations relating to domain disputes. The following events would be emitted by the Domain contract should those sensitive operations be executed.

```solidity
// A suspended domain is effectively disabled
event Suspend(
	address agent, // the address which initiated the suspension
	address indexed name, // the hash / tokenId of the domain
	bool suspended // whether the domain is suspended or reinstated
)

// A revoked domain is transferred from the registrant to the holder.
event Revoke(
	address agent, //  the address which initiated the revocation
	address indexed holder, // the address which the domain is transferred to
	uint256 indexed name // the hash / tokenId of the domain
)
```


### RainbowTable Events

Domains can be registered with only a one-way hash of the name. If the user chooses to reveal the preimage of the name, they do so using the Rainbow Table contract.

```solidity
event Revealed(
	uint256 indexed hash // the hash / tokenId of the domain which was revealed
)
```

Indexers can fetch the preimage of the revealed hash by calling `lookup(uint256 hash)` on the `RainbowTable`. This returns a set of [`Input Signals`](/concepts/name-hashing/#what-are-input-signals), which can then be decoded to reveal the ascii preimage.


### Forward Resolution Events

The `ResolverRegistry` contract keeps track of which `Resolver` contract should be used to resolve records on a given name.

```solidity
event ResolverSet(
 	// the hash of the root domain which we are setting a resolver for
	// (e.g. the root domain of subdomain.myname.avax is myname.avax)
	uint256 indexed name,

	// the hash of the domain we are setting a resolver for
	// (e.g. subdomain.myname.avax)
	uint256 indexed hash, 

	// the set of input signals we need to apply to use to hash `name`
	// into `hash`
	uint256[] path,

	// the address of the resolver contract that should be used to
	// resolve values
	address resolver,

	// the datasetId that should be used in lookup requests on the
	// resolver contract. this provides resolvers with more flexibility
	// for how they perform lookups on data.
	uint256 datasetId
)
```

A client library of the Avvy Domains system will then fetch data from the referenced resolver. See [Forward Resolution](/concepts/forward-resolution/) for more specific details on how data retrieval occurs.

`Resolver` contracts implement the [`ResolverInterface`](https://github.com/avvydomains/contracts/blob/master/contracts/ResolverInterface.sol) and should emit the following events, though Avvy Domains has no control over their deployment and so we cannot guarantee compliance with the interface.

```solidity
// A Standard Record Type has been set on the Resolver
event StandardEntrySet(
	uint256 indexed datasetId, // ID of the dataset that we set the record on
	uint256 indexed hash, // hash where the record was set (this is the hash of the domain, including subdomain)
	uint256[] path,
	uint256 key, // the Standard Record Type key for which the record has been set. for example, we use 3 for EVM addresses
	string data // the data that has been set
)

// A Custom Record Type has been set on the Resolver
event EntrySet(
	uint256 indexed datasetId, // ID of the dataset that we set the record on
	uint256 indexed hash, // hash where the record was set (this is the hash of the domain, including subdomain)
	uint256[] path,
	string key, // the custom key that the record was set on
	string data // the data that has been set
)
```


### Reverse Resolution Events

The `ReverseResolverRegistry` contract keeps track of which contracts are used for reverse resolution of records. See [Reverse Resolution](/concepts/reverse-resolution/) for more specific details on how data retrieval is performed.

Reverse Resolver contracts are maintained by the Avvy team. At the moment there is only one contract, for reversing an EVM address. In the future we hope to expand that support to other values such as validator Node IDs.

```solidity
// When a contract has been set to handle Reverse Resolution for a given Standard Record Type
event ResolverSet(
	uint256 standardKey, // the Standard Record Type
	address contractAddress // the contract that will handle reverse resolution
)
```

The `EVMReverseResolver`, which is configured for standard key `3`, emits the following event:

```solidity
event EntrySet(
	// the hash of the root domain that the entry was set on
	uint256 indexed name, 

	// the Input Signals, which must be applied to the `name`
	// to get the `hash` which the record was set on
	uint256[] path, 

	// the EVM address which reverses to the provided pair.
	address target
)
```

