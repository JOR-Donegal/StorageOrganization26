# Object Storage
One of the things I noted about file systems, is that they need a way for us humans to sort and categorise files; we need directories. We do if we're humans looking directly at the files, but that sorting information could equally be kept in a meta data structure by an application. There would be some amazing advantages to just having a flat storage system with metadata. This is how most modern cloud storage works.

We store a file on what appears to be flat storage with no directories. 

- We give the file a unique identifier. 
- We store metadata about the file, tied to its name. 

And when we want to retrieve the file, we look at the _object store_ and use the unique identifier, not an absolute path as we might with a file based system.

When I am covering AWS cloud, we look at _S3 buckets_. This is one of the most common types of object storage developers use at the moment.