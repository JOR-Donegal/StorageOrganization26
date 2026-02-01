# Block Storage

When a client computer consumes a file from its own hard drive, it uses the hardware in the drive controller to access and retrieve a block of data, these days usually 4KB minimum per block. Access to storage is comparatively slow. The computer will use _Direct Memory Access_ (DMA) for efficiency and to avoid blocking the CPU. 

Once the block of data is in memory, it is accessible to the operating system and to the user. The underlying hardware has been abstracted to the notion of a file system. The application does not “see” the block storage. The OS does however get to write directly to the _metadata_ of the hard disk. Only one OS can have this level of access; if two OS were to share access to this metadata, the disk would be quickly corrupted.

<figure>
<img src = "https://jor-donegal.github.io/StorageOrganization26/images/fig1.jpg">
<figcaption>Fig 1. Model of disk access.</figcaption>
</figure>