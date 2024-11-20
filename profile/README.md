## Hi there 👋

Crums is about efficiently proving things using cryptographic hash proofs.
While a hash may stand in for any object, we're particularly interested in
data (hash) structures that allow one to efficiently prove

- **Order of Operations.** I.e. where (at what index) does an item occur in a list
- **When.** Minimum age of an object, when was it first witnessed.
- **Differential Disclosure.** Disclose and prove only the parts you want to show, obfuscate the rest.

and enable

- **Commitment Protocols.** For e.g. at end-of-quarter, an organization commits
  to not changing the rows in their financial ledger by declaring its hash in
  their 10K filing. Any single cell in their ledger can later be efficiently proven
  to belong to the 10K's committed hash.

Among their many functions, blockchains serve as immutable historical records. Many of the concepts
and techniques (mostly via cryptographic hashproofs) used here are borrowed from blockchain technologies.
However, to the degree feasible, the methods introduced here are *not concensus driven*. Rather, the aim
is to prove things using *factuals* (or counter-factuals).

## Roadmap

### Timechain (Alpha)

The redesigned time chain uses the
[skip ledger](https://github.com/crums-io/skipledger) data (hash) structure
for linking successive blocks. This brings key improvements on the
old architecture. In particular,

- **Faster Commits.** Presently testing with 1 sec (1024 ms) blocks.  This returns a
  witness record (crumtrail) for a newly seen hash in under 3 seconds. (Dialing this
  down any further affects *geographic* scalability.) This is all possible because the chain is
- **More Compact**. Blocks are now fixed-size, only 64 bytes each. If the chain churns
  out a new block every 8 seconds, it will grow by less than a quarter GB per year.
- **Self Verifying.** The chain's state can be advertised in a compact *state proof*.
  A state proof is a synopsis of how the hash of the last block was calculated. And
  because of the way it structured, new state proofs can be validated agains old state
  proofs --- independently, off-chain.
- **Distributed.** Tho the typical user won't, anyone can spin up their own timechain.

See this project [overview](https://crums-io.github.io/timechain/)

### Open Source Server

Server-side code is released under the AGPL. The principal reason why
previous versions were never released was because the source code might've expose attack vectors I might
not have thought thru. (That's probably still true today, but I can't think of a better
way to harden the code by letting more eyeballs see it.)

#### Federated Reality

There are valid architectural reasons for having more than one timechain.
Besides their recording the order of operations, timechains are semantically opaque
to all but their individual users. There can be any number of these chains. Some may
even run in secret. And one chain may periodically commit its state (as represented
by the hash of its last block) in *another* time chain.

A timechain, on its own, can only prove the *minimum* age of its artifacts.
The chain, after all, could have been generated ahead of time. Unless.. Unless
the chain *records a hash that couldn't have been generated ahead of time*. So if a
timechain [also] records the hash of other timechains, then to be *pre*-generated,
the other timechains would also have had to be generated in advance. Thus the more
timechains record each other, the more infeasible it becomes to precompute their
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
