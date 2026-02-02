# SAN Anatomy
The SAN storage controller has several sub-systems. Controllers or their subsystems will always be redundant. There are a lot of very specialised terms, and they're used differently in different equipment and from different vendors. I'm going to describe some of those terms here.

## Front End

The front-end provides an interface between _compute_ (the host) and storage and has ports/interfaces to the physical network, it could be Ethernet, _Infiniband_ or _Fibre Channel_ and there will be multiple ports for redundancy, load-balancing or _Multipath Input Output_ (MPIO).

## Cache
Cache is critical for performance. Magnetic Hard Disk Drives (HDDs) are slow in terms of access time. Cache can dramatically improve this performance. SANs can use _hierarchical storage_, where both SSDs and DRAM are used to cache data, with HDDs providing capacity and SSDs/DRAM providing caching and performance.

## Read Operations
When data is cached, it has an associated tag, part of the main memory address used to track blocks of data in the cache. On read, the storage controller reads the tag entries to verify is the requested data is already in cache. If it is, that is a _cache hit_ and the response is immediate (in milliseconds) without any call to the backend storage system.

<figure>
<img src = "https://jor-donegal.github.io/StorageOrganization26/images/fig4.avif">
<figcaption>Fig 4. Model SAN front end cache.</figcaption>
</figure>

In the event of a _cache miss_, the backend reads data from disk and cache before a response. The read-hit ratio is the overall figure.

_Read Hit Ratio = Cache Hits / Total Reads_

<figure>
<img src = "https://jor-donegal.github.io/StorageOrganization26/images/fig5.avif">
<figcaption>Fig 5. Model SAN cache miss.</figcaption>
</figure>

When sequential reads are occurring, the cache controller will anticipate and do _pre-fetch_ or _read-ahead_, loading blocks which have not yet been requested into the cache. Where I/O requests are fixed in size fixed length prefetch matches these I/O block sizes, there can also be variable length prefetch. _Maximum prefetch_ specifies how much cache can be used for prefetch.

## Write Operations

The host writes to the SAN and receives an acknowledgement. Data could be written all the way to the _backing store_, this _write-through_ strategy gives the lowest risk of data loss or corruption, but poor performance. Data can be written to two separate caches in _cache mirroring_, to prevent data loss in the event of cache failure, but this introduces another potential issue, _cache coherency_; different, inconsistent data in different caches.

Writing to cache is obviously quicker than writing to the backing storage, the SAN controller can acknowledge the write and commit or _de-stage_ several writes to the backing store as it becomes convenient; this is a _write-back cache_ and will perform better, although any failure to write to backing storage could cause data loss or corruption.

Very large writes could bypass the cache rather than congest it. If a write exceeds the _write aside size_, it is written directly, the cache is kept free for small, random I/O. Cache can be dedicated for read and write or pooled as a _global cache_, and dynamically allocated.

In the event of power failure, cache can be maintained by battery, but on a large system, there is still the risk of the battery being expended before writes can occur. Dedicated disks can be provided for cache to write to, this is called _cache vaulting_.     

## Cache Management
The performance of cache is dependent on the quality of the management algorithms used. The _Least Recently Used_ (LRU) approach selects pages which have not been recently used and discards them first, as they are no longer needed. The _Most Recently Used_ (MRU) approach selects pages which have been used to discard, as they are no longer needed!

Pages written to cache but not to the backing store are _dirty pages_. At a certain point when many dirty pages are ready to be written, cache must be _flushed_; dirty pages written to the backing store. This is called _high-water mark flushing_. When enough pages have been flushed a cache can stop flushing, this is the _low-water mark_. Between these two levels, the cache is flushed opportunistically when the controller is otherwise idle, this is called _idle flushing_. In the event that the cache becomes 100% full and congested, _forced flushing_ occurs, where I/O may be throttled to allow the cache to clear. This will negatively effect performance.

## Back End
The backend interfaces with the storage devices over typical busses, SATA, SCSI, SAS, Fibre Channel, etc. and there may be an option to mix drives. In hierarchical storage, there may be trays of drives with different performance and functions.

There may be dual backend controllers and they have ports/interfaces to the physical drives. There will be dual ports per backend controller for redundancy and load balancing and enterprise drives may also be dual-ported.

The backend will provide some limited buffering and will perform error checking, correcting (ECC) and implement any storage strategy like RAID. 