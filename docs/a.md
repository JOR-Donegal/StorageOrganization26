# Block Storage

When a client computer consumes a file from its own hard drive, it uses the hardware in the drive controller to access and retrieve a block of data, these days usually 4KB minimum per block. Access to storage is comparatively slow. The computer will use _Direct Memory Access_ (DMA) for efficiency and to avoid blocking the CPU. 

Once the block of data is in memory, it is accessible to the operating system and to the user. The underlying hardware has been abstracted to the notion of a file system. The application does not “see” the block storage. The OS does however get to write directly to the _metadata_ of the hard disk. Only one OS can have this level of access; if two OS were to share access to this metadata, the disk would be quickly corrupted.

<figure>
<img src = "https://jor-donegal.github.io/StorageOrganization26/images/fig1.png">
<figcaption>Fig 1. Model of disk access.</figcaption>
</figure>

Similarly, when we use a network share, the file is presented as such to the application. The OS presents the file system to the application as it it were local. However, in this case, the OS does not get to edit the metadata of the backing store on the file server. In a typical Windows system, the client OS communicates with the server via a _Network Interface Card_ (NIC) and a protocol like _Server Message Block_ (SMB) and the server edits the metadata of the hard drive.

<figure>
<img src = "https://jor-donegal.github.io/StorageOrganization26/images/fig2.avif">
<figcaption>Fig 2. Model of file server access.</figcaption>
</figure>

These are both forms of _file sharing_. 

In the first case, the OS takes care of the storage, right the way down to the structures on the disk. 

In the second case, network file sharing puts an abstraction between the block storage and the OS which consumes it.

When we use a _Storage Area Network_ (SAN), we combine the two concepts. We provide to the client OS a _Logical Unit Number_ (LUN) which appears like a raw disk partition. The client OS can format this partition and can write directly to its metadata. When we talk about providing block storage, this is the concept. 

<figure>
<img src = "https://jor-donegal.github.io/StorageOrganization26/images/fig3.avif">
<figcaption>Fig 3. Model SAN access.</figcaption>
</figure>