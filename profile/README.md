## Hi there 👋

Crums is about efficiently proving things using cryptographic hash proofs.
While a hash may stand in for any object, we're particularly interested in
data (hash) structures that allow one to efficiently prove

- **Order of Operations.** I.e. where (at what index) does an item occur in a list
- **When.** Minimum age of an object, when was it first witnessed.
- **Obfuscate Parts.** Prove only the parts you want to show, obfuscate the rest.

and enable

- **Commitment Protocols.** For e.g. at end-of-quarter, an organization commits
  to not changing the rows in their financial ledger by declaring its hash in
  their 10K filing. Any single cell in their ledger can later be efficiently proven
  to belong to the 10K's committed hash.

Many concepts and techniques used here are borrowed from blockchain technologies.
But to the degree feasible, we develop tools and methods for proving things *off*-chain.
Our methods are *not concensus driven* (because they don't need to be).

## Roadmap

### Time Chain 2

The time chain is being redesigned (again). This uses the new
[skip ledger](https://github.com/crums-io/skipledger) data (hash) structure
for linking successive blocks. This should bring signficant improvements on the
old architecture. In particular,

- **Faster Commits.** It should take a user less than 15 seconds to receive a verifiable a
  witness record (crumtrail) for a newly seen hash. We could dial this down even further
  if need be. (But what'd be the point?) This is all possible because the chain is
- **More Compact**. Blocks are now fixed-size, only 68 bytes each. If the chain churned
  out a new block every 8 seconds, it would grow by less than a quarter GB per year.
- **Self Verifying.** The chain's state can be advertised in a compact *state proof*.
  A state proof is a synopsis of how the hash of the last block was calculated. And
  because of the way it structured, new state proofs can be validated agains old state
  proofs --- independently, off-chain.

See the [TC-2 design doc](https://github.com/crums-io/crums-pub/blob/main/tc2.md)

### Open Source Server

Server-side code is planned to be released under the AGPL. The principal reason why
it was never released was because the source code might've expose attack vectors I might
not have thought thru. That's probably still true today, but I can't think of a better
way to harden the code by letting more eyeballs see it.

#### Federated Reality

There are valid architectural reasons for having more than one time chain.
Besides their recording the order of operations, time chains are semantically opaque
to all but their individual users. There can be any number of these chains. Some may
even run in secret. And one chain may periodically commit its state (as represented
by the hash of its last block) in *another* time chain.

A time chain, on its own, can only prove the *minimum* age of its artifacts.
The chain, after all, could have been generated ahead of time. Unless.. Unless
the chain *records a hash that couldn't have been generated ahead of time*. So if a
time chain [also] records the hash of other time chains, then to be *pre*-generated,
the other time chains would also have had to be generated in advance. Thus the more
time chains record each other, the more infeasible it becomes to precompute their
state in some contrived collusion of chain operators. If reality requires observers,
then a federation of observers that can agree on when and what was seen is better
than a single one.

### How to Contribute

If this project excites you, please consider contributing to its cause. Drop me a
line to discuss. In a world about to be buried under an avalanche of deep fakes,
establishing the *when* of things should go a long way to establishing their
provenance.

~ Babak

< babak (at) crums (dot) io >
