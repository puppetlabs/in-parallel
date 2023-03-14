# Changelog

## [1.0.0](https://github.com/puppetlabs/in-parallel/tree/1.0.0) (2023-03-15)

[Full Changelog](https://github.com/puppetlabs/in-parallel/compare/0.1.17...1.0.0)

**Merged pull requests:**

- \(RE-15226\) Update codeowners and add standard workflows [\#20](https://github.com/puppetlabs/in-parallel/pull/20) ([yachub](https://github.com/yachub))
- \(maint\) update exists? -\> exist? for ruby 3.2 compatibility [\#19](https://github.com/puppetlabs/in-parallel/pull/19) ([tvpartytonight](https://github.com/tvpartytonight))

## [0.1.17](https://github.com/puppetlabs/in-parallel/tree/0.1.17) (2017-02-07)

[Full Changelog](https://github.com/puppetlabs/in-parallel/compare/0.1.16...0.1.17)

**Merged pull requests:**

- \(maint\) Properly handle non-parallel enumerables [\#17](https://github.com/puppetlabs/in-parallel/pull/17) ([nicklewis](https://github.com/nicklewis))

## [0.1.16](https://github.com/puppetlabs/in-parallel/tree/0.1.16) (2017-02-06)

[Full Changelog](https://github.com/puppetlabs/in-parallel/compare/0.1.15...0.1.16)

## [0.1.15](https://github.com/puppetlabs/in-parallel/tree/0.1.15) (2017-02-03)

[Full Changelog](https://github.com/puppetlabs/in-parallel/compare/0.1.14...0.1.15)

**Merged pull requests:**

- \(maint\) Avoid deadlock with large results [\#16](https://github.com/puppetlabs/in-parallel/pull/16) ([nicklewis](https://github.com/nicklewis))
- \(maint\) Revert name change of in\_parallel.rb [\#15](https://github.com/puppetlabs/in-parallel/pull/15) ([samwoods1](https://github.com/samwoods1))

## [0.1.14](https://github.com/puppetlabs/in-parallel/tree/0.1.14) (2016-08-08)

[Full Changelog](https://github.com/puppetlabs/in-parallel/compare/0.1.13...0.1.14)

**Merged pull requests:**

- \(maint\) Consistent naming of in-parallel [\#14](https://github.com/puppetlabs/in-parallel/pull/14) ([samwoods1](https://github.com/samwoods1))

# experimental_in-parallel_bump_and_tag_master - History
## Tags
* [LATEST - 6 Feb, 2017 (8e97ff25)](#LATEST)
* [0.1.16 - 6 Feb, 2017 (0d5030c3)](#0.1.16)
* [0.1.15 - 3 Feb, 2017 (ff16929c)](#0.1.15)
* [0.1.14 - 8 Aug, 2016 (ce331dbd)](#0.1.14)
* [0.1.13 - 8 Aug, 2016 (26d19934)](#0.1.13)

## Details
### <a name = "LATEST">LATEST - 6 Feb, 2017 (8e97ff25)

* (GEM) update in-parallel version to 0.1.17 (8e97ff25)

* Merge pull request #17 from nicklewis/handle-non-parallel-enumerables (dca0b0a5)


```
Merge pull request #17 from nicklewis/handle-non-parallel-enumerables

(maint) Properly handle non-parallel enumerables
```
* (maint) Properly handle non-parallel enumerables (b041b864)


```
(maint) Properly handle non-parallel enumerables

For Enumerables containing 0 or 1 items, the #each_in_parallel method
was improperly calling the block without an argument, then calling it
again properly but not returning the result of the block.

The #each method returns the Enumerable that was it was called on,
rather than the value of the block. This needs to be #map instead, to
actually return an array of the one or zero values. The tests weren't
catching this because they were effectively passing `identity` as the
block, nullifying the distinction between #each and #map.
```
### <a name = "0.1.16">0.1.16 - 6 Feb, 2017 (0d5030c3)

* (HISTORY) update in-parallel history for gem release 0.1.16 (0d5030c3)

* (GEM) update in-parallel version to 0.1.16 (27b497ea)

### <a name = "0.1.15">0.1.15 - 3 Feb, 2017 (ff16929c)

* (HISTORY) update in-parallel history for gem release 0.1.15 (ff16929c)

* (GEM) update in-parallel version to 0.1.15 (206a62fe)

* Merge pull request #16 from nicklewis/support-large-results (4d644d88)


```
Merge pull request #16 from nicklewis/support-large-results

(maint) Avoid deadlock with large results
```
* (maint) Avoid deadlock with large results (a5a9c174)


```
(maint) Avoid deadlock with large results

Previously, if the result of a process was larger than the IO buffer
size (commonly 64k), execution would deadlock until the timeout.

In this scenario, the writer would fill the buffer and block until the
reader had cleared the buffer by reading. However, the reader will only
try to read once (to get the whole result) and will only attempt to read
after the child process has exited. This causes a deadlock, as the child
can't exit because it can't finish writing, but the the reader won't
read because the child hasn't exited.

This commit fixes the watcher loop to instead IO.select() from the
available result readers and read a partial result into a buffer whenever it's
available. This ensures that the writer will never remain blocked by a
full buffer. The reader now uses IO#eof? to determine whether the child
process has exited, at which point it will process the whole result as
before.
```
* Merge pull request #15 from samwoods1/add_jjb_pipelines (72d32635)


```
Merge pull request #15 from samwoods1/add_jjb_pipelines

(maint) Revert name change of in_parallel.rb
```
* (maint) Revert name change of in_parallel.rb (327c8fd5)

### <a name = "0.1.14">0.1.14 - 8 Aug, 2016 (ce331dbd)

* (HISTORY) update in-parallel history for gem release 0.1.14 (ce331dbd)

* (GEM) update in-parallel version to 0.1.14 (d026c624)

* Merge pull request #14 from samwoods1/add_jjb_pipelines (269bc350)


```
Merge pull request #14 from samwoods1/add_jjb_pipelines

(maint) Consistent naming of in-parallel
```
* (maint) Consistent naming of in-parallel (6fbb442d)

### <a name = "0.1.13">0.1.13 - 8 Aug, 2016 (26d19934)

* Initial release.


\* *This Changelog was automatically generated by [github_changelog_generator](https://github.com/github-changelog-generator/github-changelog-generator)*
