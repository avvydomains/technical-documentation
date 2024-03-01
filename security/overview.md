---
label: Security Considerations
order: 1
---

# Security Considerations

### Domain Control

The owner of a domain has the power to modify that domain, including being able to change resolution behavior for that domain. This includes [forward resolution](/concepts/forward-resolution/) and [reverse resolution](/concepts/reverse-resolution/). This is desired behavior, but integrators should understand how this can impact their users.

For example, an integrating wallet might allow users to enter a `.avax` domain name for transfer of funds. When the user "sends" the transaction the wallet software fetches the EVM 0x address associated with the `.avax` name then sends a transaction to that 0x address. The user who controls the `.avax` name has the power to redirect those transfers of funds.


### Domain Transfers

Since users are able to transfer domains to others, we potentially can have Domain Control transferring between users. It is important for integrators (and users) to understand how & when domains can transfer to others.

**ERC721 Transfers.** The simplest example of a domain transfer occurs when a user intentionally transfers the domain to another user via ERC721 standard methods.  

**Registration Expiry.** All domains have an expiration date. When a user fails to renew their domain, there is a grace period where they can renew it. After the grace period, the domain is released via a Dutch Auction where any users can acquire the domain. If the domain is not acquired at auction, the domain becomes freely available for registration. 

**Domain Disputes.** Avvy Domains supports [Domain Disputes](https://avvy.domains/docs/domain-disputes-overview/). The outcome of a dispute can lead to the transfer of a domain between users.

Any transfer of a domain will emit an ERC721 `Transfer` event. See [Events & Indexing](/contracts/events/) for more details.


### Third Party Features

The Avvy Domains system is extensible. Domain registrants can implement custom functionality for resolution & reverse resolution of a domain. This custom functionality can include [individual ownership of subdomains](/concepts/subdomain-management/). In such cases, we have no control over how subdomain ownership is transferred. We also have no control over the events that are emitted from contracts.

In the base system, ownership is limited to the root domain (i.e. `name.avax`).


### Security Audits

Our security audits are public on the [Paladin Sec website](https://paladinsec.co/projects/avvy-domains/).
