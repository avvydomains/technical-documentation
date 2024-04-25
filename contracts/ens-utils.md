---
order: -2
label: ENS Compatibility Utils
---

# ENS Compatibility Utils

**An interface to existing ENS tooling**

Our ENSUtils contracts make it easier for developers to use existing tooling like Viem, Ethers, Wagmi, RainbowKit, and other tooling that has support for ENS functionality.



## Contract Addresses

Version 		| Contract Address
---         		| ---
Proxy (Latest Version)	| [`0x24DFa1455A75f64800BFdB2447958D2B632b94f6`](https://snowtrace.io/address/0x24DFa1455A75f64800BFdB2447958D2B632b94f6#readContract)
V2 	 		| [`0x0EDA383ED230Ab595CCb13403104575e59462202`](https://snowtrace.io/address/0x0EDA383ED230Ab595CCb13403104575e59462202#readContract)
V1          		| [`0x40b0DC99681Db9703939bd62D76F4D448ab0fdE5`](https://snowtrace.io/address/0x40b0DC99681Db9703939bd62D76F4D448ab0fdE5#readContract)


## Viem Compatibility

Set up Viem

```javascript
import { createPublicClient, http } from 'viem'
import { avalanche } from 'viem/chains'
 
const client = createPublicClient({ 
  chain: avalanche, 
  transport: http(), 
}) 
```

Next, choose one of the ENSUtils contract addresses from the list of `Contract Addresses` above. 
```javascript
// Avvy ENS Utils Proxy
const AVVY_ENS_UTILS = '0x24DFa1455A75f64800BFdB2447958D2B632b94f6'
```

Finally, you can make a call to any of the Viem ENS methods by adding `universalResolverAddress` and setting it to our ENSUtils contract:

```javascript
const avvyName = await client.getEnsName({
  address: '0x...',
  universalResolverAddress: AVVY_ENS_UTILS
})

// returns .avax name

const address = await publicClient.getEnsAddress({
  name: 'avvydomains.avax',
  universalResolverAddress: AVVY_ENS_UTILS
})

// returns 0x address

```

The following viem methods will work:

- `getEnsAddress` (forward resolution returning EVM address)
- `getEnsName` (reverse resolution)
- `getEnsAvatar` (forward resolution returning AVATAR)
- `getEnsText` (forward resolution returning standard or custom records, specified by `key`)


## Wagmi Compatibility

Wagmi ENS methods all accept a `universalResolverAddress` argument and support is similar to Viem support. In general, please see the Viem section above to understand how to use Wagmi with .avax domains.

**Specific example:**

`useEnsAddress` is a wrapper around Viem's `getEnsAddress` and can be called as follows:

```javascript
const result = useEnsAddress({
  name: 'avvydomains.avax',
  universalResolverAddress: AVVY_ENS_UTILS, 
})
```


## Ethers Compatibility

Ethers compatibility relies on setting the `ensAddress` for the network.

For example, when instantiating a JsonRpcProvider, you can provide the `ensAddress` as follows:

```javascript
const network = {
  name: networkName,
  chainId: networkChainId,
  ensAddress: AVVY_ENS_UTILS
}
const provider = new JsonRpcProvider(rpcUrl, network)
```

Where `AVVY_ENS_UTILS` is chosen from the list of ENSUtils contracts provided at the top of this document.

We can then use ethers functions related to forward resolution, such as `provider.resolveName('avvydomains.avax')`

The following methods are supported:

- `provider.resolveName(name)`
- `provider.getAvatar(name)`
- `provider.getResolver(name)`
- `resolver.getText(key)` (where key can be a numeric key to retrieve a standard record or a string to retrieve a custom record)


## Support

Need integration support? Join our [Discord](https://go.avvy.domains/discord) for technical assistance.

