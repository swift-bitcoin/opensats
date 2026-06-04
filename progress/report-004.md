# Progress Report #4

This is a copy of the quarterly progress report to be submitted to OpenSats by the end of June 2026.

## Project Updates

> Describe your progress and accomplishments since the last report. Include links to pull requests, commits, and other work.

With Mainnet activated, all tooling set for monitoring and essential Initial Block Download (IBD) optimizations in place, the focus during this past quarter shifted to filling in the gaps necessary for a stable 1.0 release.

Performance remained a subject of improvement as well as an emphasis in protocol correctness and functional parity with the Bitcoin Core reference implementation between the areas of transaction acceptance policy (standard-ness) and consensus rules.

The public Swift API was refined and documented further, particularly in what concerns the base protocol and wallet libraries. Additionally the RPC and command line interfaces were also fine tuned. Notably the configuration format was expanded to include a consistent hierarchy of program arguments, environment variables, Swift manifest or JSON files.

Below are the most notable issues/pull requests closed in the last three months organized by focus area:

### API and configuration

- Integrate Apple's Swift Configuration package
 [#546](https://github.com/swift-bitcoin/swift-bitcoin/issues/546) [#549](https://github.com/swift-bitcoin/swift-bitcoin/pull/549)
 - Cleaned up output type solver [#540](https://github.com/swift-bitcoin/swift-bitcoin/pull/540)

### Performance and monitoring

- Recreate bitcoin core caches for block index and UTXO set [#423](https://github.com/swift-bitcoin/swift-bitcoin/issues/423)
- Switch standard metrics backend from statsd to OTel [#534](https://github.com/swift-bitcoin/swift-bitcoin/issues/534) [#537](https://github.com/swift-bitcoin/swift-bitcoin/pull/537)
- Integrate Swift System Metrics [#535](https://github.com/swift-bitcoin/swift-bitcoin/issues/535)
- Updated building guide with metrics documentation [#538](https://github.com/swift-bitcoin/swift-bitcoin/pull/538)

### Node behavior

- Track peers' best known header, chainwork and last common block. Use instead of height [#531](https://github.com/swift-bitcoin/swift-bitcoin/issues/531)
- Track peers' best header and last common ancestor block [#536](https://github.com/swift-bitcoin/swift-bitcoin/pull/536)
- Replicate Bitcoin Core logic for finding the next blocks to download from peers [#533](https://github.com/swift-bitcoin/swift-bitcoin/issues/533)
- Download blocks in parallel and from various sources during IBD [#428](https://github.com/swift-bitcoin/swift-bitcoin/issues/428) [#532](https://github.com/swift-bitcoin/swift-bitcoin/pull/532)
- Auto-connect to multiple peers [#525](https://github.com/swift-bitcoin/swift-bitcoin/issues/525) [#529](https://github.com/swift-bitcoin/swift-bitcoin/pull/529)
- Single headers sync node, except when close to the headers tip[#526](https://github.com/swift-bitcoin/swift-bitcoin/issues/526) [#527](https://github.com/swift-bitcoin/swift-bitcoin/pull/527)

### Consensus

- Missing consensus rules and limits checks [#548](https://github.com/swift-bitcoin/swift-bitcoin/pull/548)
- Full block validation logic including transactions [#137](https://github.com/swift-bitcoin/swift-bitcoin/issues/137)
- Chainwork calculation (strongest, not longest chain) [#246](https://github.com/swift-bitcoin/swift-bitcoin/issues/246)

### Policy

- Standard transaction/script resource limits    [#92](https://github.com/swift-bitcoin/swift-bitcoin/issues/92)
- Standard limits, mainly sigops [#541](https://github.com/swift-bitcoin/swift-bitcoin/pull/541)
- Output types and scriptSig standard-ness [#55](https://github.com/swift-bitcoin/swift-bitcoin/issues/55)
- Standard transaction checking [#36](https://github.com/swift-bitcoin/swift-bitcoin/issues/36)
- Implement policy via mempool pre-checks [#539](https://github.com/swift-bitcoin/swift-bitcoin/pull/539)

### Bug fixes

- Detect client channel closures (crash after outgoing peer disconnection after handshake) [#573](https://github.com/swift-bitcoin/swift-bitcoin/pull/573) [#523](https://github.com/swift-bitcoin/swift-bitcoin/pull/523)

## Plans for Next Quarter *

> Outline your goals and plans for the next quarter. Be specific about what you aim to accomplish.

With the current commitment ending, the goal going forward is to keep iterating over alpha releases until reaching API stability. There's still a backlog of about 65 [issues](https://github.com/swift-bitcoin/swift-bitcoin/issues) out of which 24 are reserved for potential contributors as they are tagged with _Good First Issue_. The rest will be prioritized by impact on the package's public interface, key performance bottlenecks and other issues.

There's a plan to increase the test coverage by continuing to port data driven tests from Bitcoin Core. Same goes for benchmarking. One idea still under review is to build a GUI client to explore the usability of the framework by dog-fooding. This may compensate for the general shortage of voluntary beta testers observed so far since the project started.

New developments from the Swift open source community and Apple must be taken into account as the language is still lacking in specific aspects of system's development, namely: `OutputSpan` support, _new_ Codable and more. In the meantime we intend to increase adoption of cutting edge language features like `~Copyable` `~Escapable`, Inline Arrays, C++ interoperability annotations, …

Project's kanban board specific to this OpenSats grant [here](https://github.com/orgs/swift-bitcoin/projects/3).
