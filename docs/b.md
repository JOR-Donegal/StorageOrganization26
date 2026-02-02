# File Storage

In simple computer systems, it's possible to store Data as raw bites, directly on the storage medium. For example, when we load an operating system, we may just have a jump instruction to a sector from which we can start loading. But that approach will not scale and will not deal with complexity.

As disks became a ubiquitous storage mechanism for computers, a level of complexity was required. Although we now use the term operating system, in the 1970s and 1980s we referred to the _disk operating system_ (DOS). There was a close coupling between the _BIOS_ on the motherboard, the disk technology, and the disk operating system utilized by the end user. The unit of interaction for the end user was the file. In the world of personal computers, __config.sys__ configured the operating system, __autoexec.bat__ loaded programmes on startup, and those programmes were individual _executable_ files perhaps with their own configuration files. User data was held in unique files with well-defined extensions, to declare what those file types were. We still use extensions to this day in Windows based operating systems. A __.bat__ file is still a list of instructions that can be carried out at the command prompt. A __.doc__ file is probably a Microsoft Word file. 

Notably we can use extensions in Linux to denote file types to us human users. But in Linux they have no significance for the operating system.

Even in the simplest operating system, we need a way of tracking and finding those files. We need a _directory listing_, a list of all the files, some properties, and a pointer as to where to find them. We use the term _metadata_ to describe this kind of information. Most files will be bigger than a single sector, in these cases we will need some sort of pointer array as to where to find the sequence of sectors which makes up the file.

Where we have many files, we need to sort them based on some non-arbitrary relevance. In an office, we would group documents into box files. In a file system we group into _directories_. This way of doing things grew organically since the 1970s. It does not scale well and unless users are very disciplined it quickly becomes unmanageable. And an unmanaged file system is a serious risk under GDPR. We should no longer base anything other than trivial storage on this simple way of holding data.

There has been a long history a file system types, and in a later set of notes, I'll deal with the more important ones and some of their characteristics.
