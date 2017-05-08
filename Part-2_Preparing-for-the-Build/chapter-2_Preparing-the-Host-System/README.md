# 2.2. [Host System Requirements](http://www.linuxfromscratch.org/lfs/view/stable/chapter02/hostreqs.html)

## Versions
Bash-3.2 (/bin/sh should be a symbolic or hard link to bash)
Binutils-2.17 (Versions greater than 2.27 are not recommended as they have not been tested)
Bison-2.3 (/usr/bin/yacc should be a link to bison or small script that executes bison)
Bzip2-1.0.4
Coreutils-6.9
Diffutils-2.8.1
Findutils-4.2.31
Gawk-4.0.1 (/usr/bin/awk should be a link to gawk)
GCC-4.7 including the C++ compiler, g++ (Versions greater than 6.3.0 are not recommended as they have not been tested)
Glibc-2.11 (Versions greater than 2.25 are not recommended as they have not been tested)
Grep-2.5.1a
Gzip-1.3.12
Linux Kernel-2.6.32
M4-1.4.10
Make-3.81
Patch-2.5.4
Perl-5.8.8
Sed-4.1.5
Tar-1.22
Texinfo-4.7
Xz-5.0.0

### To see whether your host system has all the appropriate versions, and the ability to compile programs, run the following: `version-check.sh`

### Also check for some library consistency:
library-check.sh`


# 2.4. [Creating a New Partition](http://www.linuxfromscratch.org/lfs/view/stable/chapter02/creatingpartition.html)

## Requirements
* minimal partition size: >= 6 GB
* recommended partition size: 20 GB
    * root partition: 10 GB (50%)
    * swap partition: 2 * RAM (e.g. 8 GB RAM = 16 GB) ... although 2 GB is typically sufficient
    * GRUB BIOS partition: (1) GUID Partition Table (GPT): typically 1 MB
    * convenience partitions (i.e. not required):
        * /boot – Highly recommended. Use this partition to store kernels and other booting information. To minimize potential boot problems with larger disks, make this the first physical partition on your first disk drive. A partition size of 100 megabytes is quite adequate.
        * /home – Highly recommended. Share your home directory and user customization across multiple distributions or LFS builds. The size is generally fairly large and depends on available disk space.
        * /usr – A separate /usr partition is generally used if providing a server for a thin client or diskless workstation. It is normally not needed for LFS. A size of five gigabytes will handle most installations.
        * /opt – This directory is most useful for BLFS where multiple installations of large packages like Gnome or KDE can be installed without embedding the files in the /usr hierarchy. If used, 5 to 10 gigabytes is generally adequate.
        * /tmp – A separate /tmp directory is rare, but useful if configuring a thin client. This partition, if used, will usually not need to exceed a couple of gigabytes.
        * /usr/src – This partition is very useful for providing a location to store BLFS source files and share them across LFS builds. It can also be used as a location for building BLFS packages. A reasonably large partition of 30-50 gigabytes allows plenty of room.

> Remember the designation of the new partition (e.g., sda5). This book will refer to this as the "LFS partition". Also remember the designation of the swap partition. These names will be needed later for the /etc/fstab file.

> If swapping becomes a normal occurrence, the best solution is to purchase more RAM for your system.

> Any separate partition that you want automatically mounted upon boot needs to be specified in the []/etc/fstab](http://www.linuxfromscratch.org/lfs/view/stable/chapter08/fstab.html).


# 2.5. [Creating a File System on the Partition](http://www.linuxfromscratch.org/lfs/view/stable/chapter02/creatingfilesystem.html)

## [Filesystem](http://en.wikipedia.org/wiki/Comparison_of_file_systems)
* ext2: is suitable for small partitions that are updated infrequently such as /boot.
* ext3: is an upgrade to ext2 that includes a journal to help recover the partition's status in the case of an unclean shutdown. It is commonly used as a general purpose file system.
* ext4: is the latest version of the ext file system family of partition types. It provides several new capabilities including nano-second timestamps, creation and use of very large files (16 TB), and speed improvements.

#### Root partition should be *ext4*
`mkfs -v -t ext4 /dev/<xxx>`

#### Swap partition
`mkswap /dev/<yyy>`


# 2.6. [Setting The $LFS Variable](http://www.linuxfromscratch.org/lfs/view/stable/chapter02/aboutlfs.html)

`export LFS=/mnt/lfs`


# 2.7. [Mounting the New Partition](http://www.linuxfromscratch.org/lfs/view/stable/chapter02/mounting.html)  

### Create the mount point and mount the LFS file system by running:
```bash
mkdir -pv $LFS
mount -v -t ext4 /dev/<xxx> $LFS
```

### If using multiple partitions for LFS (e.g., one for / and another for /usr), mount them using:
```bash
mkdir -pv $LFS
mount -v -t ext4 /dev/<xxx> $LFS
mkdir -v $LFS/usr
mount -v -t ext4 /dev/<yyy> $LFS/usr
```

### If you are using a swap partition, ensure that it is enabled using the `swapon` command:
```bash
/sbin/swapon -v /dev/<zzz>
```
