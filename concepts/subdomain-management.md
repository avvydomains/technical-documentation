---
order: -5
---

# Subdomain Management

The main registration system from Avvy Domains supports ownership of the root domain only. 

For example, in the main system a user can register `myname.avax` but cannot register `subdomain.myname.avax`.

Management of subdomains such as `subdomain.myname.avax` is handled by Resolvers & Reverse Resolver contracts. The system has reasonable default settings and provides developers with a flexible interface for custom functionality.

### Forward Resolution for Subdomains

Forward Resolution for a name is handled by a Resolver contract. The Default Resolver allows the owner of a name to set records on that name or on any subdomain.

Developers can implement a custom Resolver contract to suit their needs. For example, a custom Resolver could implement the ERC721 spec, granting users ownership of subdomains & allowing owners to set records on the custom Resolver.

Custom Resolver contracts should implement the [`ResolverInterface`](https://github.com/avvydomains/contracts/blob/master/contracts/ResolverInterface.sol)

### Reverse Resolution 

Reverse Resolution for names are handled by Reverse Resolver contracts, which are deployed by the system. The `ReverseResolverRegistry` contract is responsible for authorizing transactions which set reverse records. The default authorization mechanism simply checks whether the domain registration is valid & whether the user is the owner of the root domain.

Developers can implement a custom authorization contract to determine whether a given `0x` address is authorized to set a reverse record on a given subdomain. This can, for example, enable developers to implement custom subdomain registries.

Custom authorization contracts should implement the [`ReverseResolverAuthenticatorInterface`](https://github.com/avvydomains/contracts/blob/master/contracts/ReverseResolverAuthenticatorInterface.sol).

### Examples

An example project which [implements a custom subdomain registry is available here](https://github.com/avvydomains/integration-examples/tree/master/nft-resolver)
