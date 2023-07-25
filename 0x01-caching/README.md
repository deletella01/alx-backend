## Caching

The average memory reference time is T= m * T_{m} + T_{h} + E
where:
 m = miss ratio = 1 - (hit ratio)
 T_{m} = time to make a main memory access when there is a miss (or, with multi-level cache, average memory reference time for the next-lower cache)
 T_{h}= the latency: the time to reference the cache (should be the same for hits and misses)
E = various secondary effects, such as queuing effects in multiprocessor systems

There are two primary figures of merit of a cache: the latency and the hit ratio. There are also a number of secondary factors affecting cache performance.

The "hit ratio" of a cache describes how often a searched-for item is actually found in the cache. More efficient replacement policies keep track of more usage information in order to improve the hit rate (for a given cache size).

The "latency" of a cache describes how long after requesting a desired item the cache can return that item (when there is a hit). Faster replacement strategies typically keep track of less usage informationor, in the case of direct-mapped cache, no informationto reduce the amount of time required to update that information.

Each replacement strategy is a compromise between hit rate and latency.

Hit rate measurements are typically performed on benchmark applications. The actual hit ratio varies widely from one application to another. In particular, video and audio streaming applications often have a hit ratio close to zero, because each bit of data in the stream is read once for the first time (a compulsory miss), used, and then never read or written again. Even worse, many cache algorithms (in particular, LRU) allow this streaming data to fill the cache, pushing out of the cache information that will be used again soon (cache pollution).

Other things to consider:
- Items with different cost: keep items that are expensive to obtain, e.g. those that take a long time to get.
- Items taking up more cache: If items have different sizes, the cache may want to discard a large item to store several smaller ones.
- Items that expire with time: Some caches keep information that expires (e.g. a news cache, a DNS cache, or a web browser cache). The computer may discard items because they are expired. Depending on the size of the cache no further caching algorithm to discard items may be necessary.

Various algorithms also exist to maintain cache coherency. This applies only to situation where multiple independent caches are used for the same data (for example multiple database servers updating the single shared data file).
