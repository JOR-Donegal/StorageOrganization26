# Introduction

!!! abstract "Storage Organization"

There are layers of complexity in understanding how a computer organizes and accesses storage. We are going to look through this complexity, identifying the levels at which we can understand storage and defining a common vocabulary of terms we can use to describe it.

When we have a large, multi-disk storage device, we can divide up the physical disks into multiple _volumes_ and use these volumes separately. Or we can aggregate a number of disks together to appear like a single volume. The first new term is _volume_. Think of a volume like an empty bookcase with no shelves.

When we looked at the theory of how hard disks work, we discovered that disks have a topology with cylinders heads and sectors. When we save data to a disk, The smallest increment we can physically save is to one of these sectors. Sectors were traditionally 512 bytes, but on a more modern system will be 4,096 bytes. The smallest part of the disc you can write to is one of these sectors. On a modern system, even these 4 KB sectors look very small. We may aggregate sectors together to make a larger, smallest block. For example, if we aggregate 8 sectors together, the smallest unit we can read or write to becomes 32 kilobytes. Windows used to call this a _cluster_. When we share what looks like a disk (e.g. something we can format) this is _block storage_.

We can logically break up a volume and we call this _partitioning_. We will look at two partitioning systems. When we partition a volume, think of that like adding shelves 2 are empty bookcase.

Finally, each partition needs a _file system_ before we can store files on it, we will look at several types of file system. Continuing our analogy, the file system would be like an indexing system for the books on the shelves. Like for example the Dewey system in libraries. And we call this way of looking at storage, _file storage_. 