---
title: "5 SYSTEM CALLS FOR THE FILE SYSTEM"
date: "2018-10-07T13:00:00+08:00"
---

The last chapter described the internal data structures for the file system and the algorithms that manipulate them. This chapter deals with system calls for the file system, using the concepts explored in the previous chapter. It starts with system calls for accessing existing files, such as *open*, *read*, *write*, *lseek*, and *close*, then presents system calls to create new files, namely, *creat* and *mknod*, and then examines the system calls that manipulate the inode or that maneuver through the file system: *chdir*, *chroot*, *chown*, *chmod*, *stat*, and *fstat*. It investigates more advanced system calls: *pipe* and *dup* are important for the implementation of pipes in the shell; *mount* and *umount* extend the file system tree visible to users; *link* and *unlink* change the structure of the file system hierarchy. Then, it presents the notion of file system abstractions, allowing the support of various file systems as long as they conform to standard interfaces. The last section in the chapter covers file system maintenance. The chapter introduces three kernel data structures: the file table, with one entry allocated for every opened file in the system, the user file descriptor table, with one entry allocated for every file descriptor known to a process, and the mount table, containing information for every active file system.

Figure 5.1 shows the relationship between the system calls and the algorithms described previously. It classifies the system calls into several categories, although some system calls appear in more than one category:

* System calls that return file descriptors for use in other system calls;
* System calls that use the *namei* algorithm to parse a path name;
* System calls that assign and free inodes, using algorithms *ialloc* and *ifree*;
* System calls that set or change the attributes of a file;
* System calls that do I/O to and from a process, using algorithms *alloc*, *free*, and the buffer allocation algorithms;
* System calls that change the structure of the file system;
* System calls that allow a process to change its view of the file system tree.

![figure 5.1](/linux/img/bach/figure5.1.jpg)

**Figure 5.1.** File System Calls and Relation to Other Algorithms