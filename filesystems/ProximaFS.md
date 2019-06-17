# ProximaFS
A simple filesystem for OpenComputers.

## Notes
All integers are little endian. Root is always inode 0. OSDI partition ID is `proxima*`

## Layout of ProximaFS
The first logical sector always contains an x86 loop (`EB FE 90`) at the very beginning, and the rest of the filesystem info.

```c
struct ProximaFS_BS {
	unsigned char bootcode[3];
	unsigned char signature[8]; // proxima*
	unsigned char superblock_size; //sectors
	unsigned short superblock_entries; //Number of entries. Not all are allocated.
	unsigned char sector_size; // Multiply by 32.
};
```

The superblock contains the offset and size of each inode, in sectors. The structure of a superblock entry is as follows:

```c
struct ProximaFS_SuperblockEnt {
	unsigned short inode_offset; //Sectors
	unsigned short inode_size; //Sectors
	unsigned char inode_byte_offset; //Multiply by 4
};
```
An entry with an inode size of 0 is unallocated.

An inode is as follows:

```c
struct ProximaFS_Inode {
	unsigned short mode;
	unsigned char inode_name[16];
	unsigned char owner;
	unsigned char group;
	unsigned short parent;
	unsigned short fsize;
};
```

Inodes use a 12.4 format, and as such, an entry called "I_want_die.txt" is stored as `I_want_die<null><null>txt<null>`
