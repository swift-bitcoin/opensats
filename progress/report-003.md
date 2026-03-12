# Progress Report #3

This is a copy of the quarterly progress report to be submitted to OpenSats by the end of March 2026.

## Project Updates

> Describe your progress and accomplishments since the last report. Include links to pull requests, commits, and other work.

The focus this last quarter was primarily on three general areas:
- Activating the mainnet chain selection option, testing and fixing any additional protocol issues not identified during the testnet phase.
- Profiling and benchmarking the performance of the Initial Block Download (IBD) _as is_ for comparison after optimizations are introduced.
- Optimizing IBD and other related functionality while verifying performance increases.

On the mainnet activation front the following tasks were executed:

- Mainnet consensus chain parameters configured. [#492](https://github.com/swift-bitcoin/swift-bitcoin/issues/492) [#500](https://github.com/swift-bitcoin/swift-bitcoin/pull/500)

- Mainnet chain selection configuration and command line argument made default and honored. [#500](https://github.com/swift-bitcoin/swift-bitcoin/pull/500)

- Auto-connect to peers from seeded nodes (hard-coded). [#500](https://github.com/swift-bitcoin/swift-bitcoin/pull/500)

- Full compatibility with Bitcoin Core block file format. [#494](https://github.com/swift-bitcoin/swift-bitcoin/pull/494) [#499](https://github.com/swift-bitcoin/swift-bitcoin/pull/499)

- Temporarily accept orphan headers to allow for parallelism. [#497](https://github.com/swift-bitcoin/swift-bitcoin/issues/497) [#498](https://github.com/swift-bitcoin/swift-bitcoin/issues/498) [#501](https://github.com/swift-bitcoin/swift-bitcoin/pull/501)

For benchmarking the following tasks were carried:

- Better metrics sent to _statsd_ to monitor IBD performance using Graphite. [#465](https://github.com/swift-bitcoin/swift-bitcoin/pull/465) [#516](https://github.com/swift-bitcoin/swift-bitcoin/pull/516)

- Reindex utility (offline) and RPC command. [#476](https://github.com/swift-bitcoin/swift-bitcoin/issues/476) [#486](https://github.com/swift-bitcoin/swift-bitcoin/pull/486)

- Benchmarks for _get chain tips_ and _reindex from block files_ using continuous clock. [#496](https://github.com/swift-bitcoin/swift-bitcoin/issues/496)#issuecomment-3745714202 [#495](https://github.com/swift-bitcoin/swift-bitcoin/issues/495)

- Repeated profiling using Instruments and flame graphs to identify bottlenecks during IBD and reindex. [#465](https://github.com/swift-bitcoin/swift-bitcoin/pull/465)

- Added some performance tests to check certain operations complete under specified time limit [#522](https://github.com/swift-bitcoin/swift-bitcoin/pull/522)

Several improvements were made with direct impact on performance:

- Full in-memory block index with persistent DB backing. [#496](https://github.com/swift-bitcoin/swift-bitcoin/issues/496) [#504](https://github.com/swift-bitcoin/swift-bitcoin/pull/504)

- Full in-memory chain state with persistent DB backing. [#511](https://github.com/swift-bitcoin/swift-bitcoin/pull/511) [#512](https://github.com/swift-bitcoin/swift-bitcoin/pull/512)

- Adjustable cache facility for stored blocks. [#518](https://github.com/swift-bitcoin/swift-bitcoin/pull/518)

- Block disk storage serialization with actors and task chaining. [#517](https://github.com/swift-bitcoin/swift-bitcoin/pull/517) [#518](https://github.com/swift-bitcoin/swift-bitcoin/pull/518)

- Assume valid evaluation re-implemented and streamlined. [#514](https://github.com/swift-bitcoin/swift-bitcoin/pull/514) [#516](https://github.com/swift-bitcoin/swift-bitcoin/pull/516)

- Block index skip list with same deterministic formula as Bitcoin Core. [#515](https://github.com/swift-bitcoin/swift-bitcoin/pull/515) [#519](https://github.com/swift-bitcoin/swift-bitcoin/pull/519)

- Partial Swift Span adoption (more required `span` functionality coming in Swift 6.3+) [#475](https://github.com/swift-bitcoin/swift-bitcoin/pull/475)

- Span annotations for C interoperability with `libsecp256k1`. [#391](https://github.com/swift-bitcoin/swift-bitcoin/pull/391) [#475](https://github.com/swift-bitcoin/swift-bitcoin/pull/475)

- Partial adoption of official Swift Binary Parsing (framework still in development phase). [#390](https://github.com/swift-bitcoin/swift-bitcoin/pull/390) [#470](https://github.com/swift-bitcoin/swift-bitcoin/pull/470)

- Custom UInt256 type based on new Swift's Standard `UInt128` type. [#521](https://github.com/swift-bitcoin/swift-bitcoin/pull/521) [#522](https://github.com/swift-bitcoin/swift-bitcoin/pull/522)

Other notable additions outside of the main areas of focus:

- Miniscript DSL expanded with wrapper combination shortcuts and better test coverage. [#502](https://github.com/swift-bitcoin/swift-bitcoin/issues/502) [#503](https://github.com/swift-bitcoin/swift-bitcoin/pull/503) [#505](https://github.com/swift-bitcoin/swift-bitcoin/pull/505)

- First nteractive tutorials covering Bitcoin Crypto module. [#506](https://github.com/swift-bitcoin/swift-bitcoin/pull/506) [#509](https://github.com/swift-bitcoin/swift-bitcoin/pull/509)

- Idiomatic blockchain API. [#513](https://github.com/swift-bitcoin/swift-bitcoin/pull/513)

## Plans for Next Quarter *

> Outline your goals and plans for the next quarter. Be specific about what you aim to accomplish.

For next quarter the goal continues to be to achieve somewhat decent mainnet performance (as close as possible to Bitcoin Core's) using the best tools available from the Swift language and ecosystem.
Additionally aim to continue to gear towards a 1.0 release with a stable well-documented API.
 
- Keep profiling IBD and re-index processes to identify slow code paths that may be optimized.
- Optimize serialization and binary parsing of key data types.
- Optimize use of space (storage) for UTXOs.
- Download both headers and blocks in parallel, simultaneously from multiple peers.
- Revisit auto-connect and handshake to improve reliability (some nodes disconnecting unexpectedly).
- Attempt to utilize fixed inline arrays and fixed-width 256-bit integers where possible (and and proven useful).
- Continue to explore the current public API and document with interactive tutorials.

Project's kanban board specific to this OpenSats grant [here](https://github.com/orgs/swift-bitcoin/projects/3).
