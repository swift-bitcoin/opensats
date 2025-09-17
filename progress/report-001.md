# Progress Report #1

This is a copy of the quarterly progress report to be submitted to OpenSats by the end of September 2025.

## Project Updates

> Describe your progress and accomplishments since the last report. Include links to pull requests, commits, and other work.

The primary goal for this initial quarter was to start syncing the "testnet" blockchain. The consensus parameters for "Testnet 4" were configured [#379](https://github.com/swift-bitcoin/swift-bitcoin/pull/379) and all special rules of BIP94 were implemented [#406](https://github.com/swift-bitcoin/swift-bitcoin/pull/406).

A [guide](https://swiftbitcoin.org/docs/documentation/bitcoin/testnet) was written to facilitate running/testing out Swift Bitcoin alongside a controlled _dockerized_ Core instance. The configuration file format and the daemon's command line arguments were improved to accept a log level and the all important chain selection (network) value [#385](https://github.com/swift-bitcoin/swift-bitcoin/pull/385) [#403](https://github.com/swift-bitcoin/swift-bitcoin/pull/403).

During the initial synchronization attempts multiple issues and missing functionality were identified and subsequently fixed. Some of the more relevant fixes are:

- Missing persistent block undo data [#420](https://github.com/swift-bitcoin/swift-bitcoin/pull/420)
- Lack of headers-first IBD strategy [#416](https://github.com/swift-bitcoin/swift-bitcoin/pull/416)
- Poor support for chain reorganizations [#430](https://github.com/swift-bitcoin/swift-bitcoin/pull/430)
- Incomplete time-lock implementation [#443](https://github.com/swift-bitcoin/swift-bitcoin/pull/443)
- Incomplete implementation of BIP 130 [#408](https://github.com/swift-bitcoin/swift-bitcoin/pull/408)
- Anchor outputs and several consensus related bug fixes [#414](https://github.com/swift-bitcoin/swift-bitcoin/pull/414) 

Performance and traceability was also proven to be an area in need of focus with many improvements and refactors affecting file system, database persistence and networking:

- Re-implementation of LMDB bindings using non-copyable types [#381](https://github.com/swift-bitcoin/swift-bitcoin/pull/381)
- Move block validation to a concurrent background queue [#422](https://github.com/swift-bitcoin/swift-bitcoin/pull/422)
- Upgraded `libsecp256k1` integration [#421](https://github.com/swift-bitcoin/swift-bitcoin/pull/421)

On the library side of things the public API was completely streamlined and documented [#374](https://github.com/swift-bitcoin/swift-bitcoin/pull/374) [375](https://github.com/swift-bitcoin/swift-bitcoin/pull/375). A pre-release build was issued and submitted to the [Swift Package Index](https://swiftpackageindex.com/swift-bitcoin/swift-bitcoin) for publication with new unified [DocC documentation](https://swiftpackageindex.com/swift-bitcoin/swift-bitcoin/0.1.1/documentation) for users and automatically generated developer documentation. An announcement was made on the [Swift Forums](https://forums.swift.org/t/swift-bitcoin-full-node-library/75431/9) as well as on social media in an effort to promote collaboration.

A [project board](https://github.com/orgs/swift-bitcoin/projects/2) was set up at the beginning of the grant period to track all work items covered by the commitment in real time. As of this write up, over 50 work items have been completed while about 25 items remain either in backlog or in progress with more to be added in the upcoming weeks. The project itself has over [80 recorded GitHub Issues](https://github.com/swift-bitcoin/swift-bitcoin/issues).

## Plans for Next Quarter *

> Outline your goals and plans for the next quarter. Be specific about what you aim to accomplish.

The main goals continue to be:

1) Bitcoin Node (`bcnode`) support of Testnet 4 which includes initial block download, keeping up with new blocks, handling reorgs and relaying transactions.
2) Bitcoin Utility (`bcutil`) capabilities to verify the correct operation of node instances via RPC commands and off-chain operations. This includes listing recorded reorgs and submitting raw transactions.
3) Library API covering all base bitcoin protocol and wallet functionality in a way that is fully compatible with Testnet 4. For this we need to keep making sure we follow the official Swift Language [API Design Guidelines](https://www.swift.org/documentation/api-design-guidelines/) in order to provide a solid 1.0 release that's both idiomatic and ergonomic.

We want users to be able to download Swift Bitcoin (Linux Docker images and binaries [already being provided](https://hub.docker.com/r/swiftbitcoin/swift-bitcoin) with each release) and have a testnet instance that they can sync and interact in a way that's similar to Bitcoin Core. By the same token we want developers to use Swift Bitcoin in their apps whether it be building a simple wallet or an e-commerce site. We already received some positive feedback (privately and publicly on our [X account](https://x.com/SwiftBitcoinOrg)) from daredevil iOS developers integrating the library into experimental products. We'd like to give those developers a proper release and a chance to contribute back in a positive feedback loop. 

To that effect here's a few GitHub issues to highlight from the [Kanban board](https://github.com/orgs/swift-bitcoin/projects/2):

- [Fully sync live Testnet 4 chain](https://github.com/swift-bitcoin/swift-bitcoin/issues/405)
- [RPC command to get active and historical chain tips](https://github.com/swift-bitcoin/swift-bitcoin/issues/429)
- [Relay blocks and transactions to relevant peers](https://github.com/swift-bitcoin/swift-bitcoin/issues/427)
- [Testnet 4 seed nodes](https://github.com/swift-bitcoin/swift-bitcoin/issues/401)

Behind the scenes on the purely technical side we'd also like to integrate Apple's [Swift Metrics](https://github.com/apple/swift-metrics) to get a better picture of the network client's behavior and operation through either Open Telemetry or Prometheus. There's also a new official [binary parser](https://github.com/apple/swift-binary-parsing) that might help us boost our serialization/deserialization code.

One additional somewhat self-imposed requirement would be to start incorporating many of the new [Swift 6.2](https://www.swift.org/blog/swift-6.2-released/) (released September 16, 2025) features that can greatly impact our package's performance like [inline arrays](https://developer.apple.com/documentation/swift/inlinearray) and spans. A full refactor of the affected code may not be possible but a partial implementation should be sufficient to make a dent in performance.
