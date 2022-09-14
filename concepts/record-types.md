---
order: -2
---

# Records & Record Types

A `.avax` domain is a type of database. Users can use the system to link pieces of information to their `.avax` name. We call these pieces of information `Records`.

A client of the system will usually have one of two goals:

- Given a `.avax` name, let me find an associated `Record`
- Given a `Record`, let me find the associated `.avax` name

These two operations are the core of our system. The operations are referred to as `Forward Resolution` and `Reverse Resolution`, respectively.

!!!
You can think of Avvy Domains as a key-value database, where the key is either a number or a string and the value is any string.
!!!

### Record Types


Avvy Domains supports two types of `Records`: 

- **Standard Records** are identified by a number & accompanied by a specification. [A list of Standard Records is maintained in our Client Common library](https://github.com/avvydomains/client-common/blob/master/records/records.json).

- **Custom Records** are identified by a string & have no formal specification. Users of the system are free to define their own specifications or use the tool however they wish.
