# Progress Report #2

This is a copy of the quarterly progress report to be submitted to OpenSats by the end of December 2025.

## Project Updates

> Describe your progress and accomplishments since the last report. Include links to pull requests, commits, and other work.

Having already achieved testnet synchronization, the main goal for this second quarter was to increase node stability at the chain tip while keeping up with incoming blocks and transactions.

To that effect here's some relevant tickets laid out by the previous report which has since been closed:

- [Fully sync live Testnet 4 chain](https://github.com/swift-bitcoin/swift-bitcoin/issues/405)
- [RPC command to get active and historical chain tips](https://github.com/swift-bitcoin/swift-bitcoin/issues/429)
- [Testnet 4 seed nodes](https://github.com/swift-bitcoin/swift-bitcoin/issues/401)

Tooling and monitoring has been beefed up in preparation for the next phase of optimization:

- [Metrics Framework](https://github.com/swift-bitcoin/swift-bitcoin/issues/372)
- [Remote Profiling](https://github.com/swift-bitcoin/swift-bitcoin/pull/465)
- [Standardized Benchmarking](https://github.com/swift-bitcoin/swift-bitcoin/issues/271)

Integration of powerful new [Swift 6.2](https://www.swift.org/blog/swift-6.2-released/) features has already started with [#470](https://github.com/swift-bitcoin/swift-bitcoin/pull/470) and [#391](https://github.com/swift-bitcoin/swift-bitcoin/issues/391) with more features like [inline arrays](https://developer.apple.com/documentation/swift/inlinearray) being implemented real soon.

On the library side of things several patch releases were issued and are now available [on GitHub](https://github.com/swift-bitcoin/swift-bitcoin/releases) as well as on the [Swift Package Index](https://swiftpackageindex.com/swift-bitcoin/swift-bitcoin) complete with user and developer documentation. After fixing [481](https://github.com/swift-bitcoin/swift-bitcoin/pull/481) and [478](https://github.com/swift-bitcoin/swift-bitcoin/pull/478) the package is now considered stable to include in other projects as a dependency using semantic version specifiers.

Other relevant work items from the aggregated change log of the last 3 releases:

* [Correctly using median time past (BIP113)](https://github.com/swift-bitcoin/swift-bitcoin/pull/443)
* [Accurate verification progress estimation](https://github.com/swift-bitcoin/swift-bitcoin/pull/455)
* [Comprehensive tests for complex reorganization with chain re-activation](https://github.com/swift-bitcoin/swift-bitcoin/pull/458)
* [Incoming peer disconnection now detected immediately](https://github.com/swift-bitcoin/swift-bitcoin/pull/460)
* [Unlimited dynamic P2P client services](https://github.com/swift-bitcoin/swift-bitcoin/pull/461)
* [Returning sequential peer ID when connecting manually](https://github.com/swift-bitcoin/swift-bitcoin/pull/462)
* [Improved algorithm to find the next block to validate](https://github.com/swift-bitcoin/swift-bitcoin/pull/464)
* [Auto-connect to peers at launch](https://github.com/swift-bitcoin/swift-bitcoin/pull/469)
* [Testnet 4 is now the default network](https://github.com/swift-bitcoin/swift-bitcoin/pull/472)
* [Aligned mempool checks including finality](https://github.com/swift-bitcoin/swift-bitcoin/pull/474)
* [Multiple fixes involving relative time locks, compact blocks, IBD and testnet 4 synchronization](https://github.com/swift-bitcoin/swift-bitcoin/pull/454)

A [project board](https://github.com/orgs/swift-bitcoin/projects/2) was set up at the beginning of the grant period to track all work items covered by the commitment in real time. As of this writeup, a total of over 107 work items have been completed (57 in the last quarter) while about 5 items remain either in backlog or in progress to be completed in the upcoming days.

The project itself has over [60 recorded GitHub Issues](https://github.com/swift-bitcoin/swift-bitcoin/issues) (down from about 80+) with many tagged as _Good First Issue_ to encourage developer contributions.

## Plans for Next Quarter *

> Outline your goals and plans for the next quarter. Be specific about what you aim to accomplish.

In the upcoming months we would like to gear towards mainnet chain validation and synchronization. For this we need to ramp up our monitoring and get optimizing as the current implementation remains too slow for the almost 1TB of historical transaction volume to date.

Some action points include:

 - Measure and log partial IBD performance with purpose-made RPC commands.
 - Establish a baseline for multiple benchmarks using CI.
 - Additional performance tests with recorded execution times.
 - Profiler flame graph analysis and marking of performance bottlenecks within the codebase.
 - Record and chart IBD _statsd_ metrics including some time measurements.
 - Better debug logging messages to help diagnose slowness and other issues.
 - Implement proper cache facilities for the block index and UTXO set as well as stored block/undo data. 
 - Rewrite binary parsers using safer and more efficient span types.
 - Port over more data driven tests from Core and increase overall coverage.
 - Keep dog-fooding the library with the CLI utility as well as some rough GUI.

The latest iterations of Swift already provides us with some optimizing and safety opportunities. As the language continues to evolve into a mature multi-platform language with systems development capabilities we want Swift Bitcoin to take full advantage and be the best example of how these technologies are made for one another.

We would love for users to test drive Swift Bitcoin – using the [Docker Images](https://hub.docker.com/r/swiftbitcoin) provided with each release or installing on Mac with [Mint](https://github.com/yonaskolb/Mint) – and have a daemon instance at their disposal to interact with in a way similar to Bitcoin Core. By the same token we want developers to use Swift Bitcoin in their apps whether it be building a simple wallet or an e-commerce site. We already received some positive feedback from intrepid iOS developers integrating the library into experimental vibe-coded products. We'd like to offer those developers a proper stable release and a chance to contribute back to the project in a positive feedback loop. 

