🗃️ Customized Virtual File System in C
This project is a simplified, custom-built virtual file system implemented in C, inspired by the Linux File System. It supports basic file operations such as create, read, write, open, close, ls, and more — allowing users to interact with files in a simulated environment using terminal-like commands.

🛠️ Features
Create and manage regular files

Open files in different modes (read, write, read+write)

Read/write data into files

View file information (stat, fstat)

Maintain file permissions and reference counts

Truncate, delete, and seek within files

Command help system (man, help)

📁 Data Structures Used
SUPERBLOCK
Keeps track of the total and free inodes (files).

c
Copy
Edit
typedef struct superblock {
    int TotalInodes;
    int FreeInode;
} SUPERBLOCK;
INODE
Describes each file with metadata and data buffer.

c
Copy
Edit
typedef struct inode {
    char FileName[50];
    int inodeNumber;
    int FileSize;
    int FileActualSize;
    int FileType;
    char *Buffer;
    int LinkCount;
    int ReferenceCount;
    int permission;
    struct inode *next;
} INODE;
FILETABLE
Stores the mode and offset for opened files.

c
Copy
Edit
typedef struct filetable {
    int readoffset;
    int writeoffset;
    int count;
    int mode;
    PINODE ptrinode;
} FILETABLE;
UFDT
User File Descriptor Table to manage open files.

c
Copy
Edit
typedef struct ufdt {
    PFILETABLE ptrfiletable;
} UFDT;
🧑‍💻 How It Works
On startup, the virtual file system initializes memory structures.

File operations (like create, read, write) can be executed via command-line input.

Each file is associated with an inode, tracked in a linked list.

Open files are managed using a UFDT array.

📌 Commands Supported
Command	Description
create	Create a new regular file
open	Open an existing file with a mode
read	Read data from a file
write	Write data into a file
ls	List all files
stat	Display file information using name
fstat	Display file information using descriptor
truncate	Clear contents of a file
rm	Delete a file
lseek	Change the read/write offset of a file
close	Close a specific file
closeall	Close all open files
man	Get usage details for a command
help	List all available commands
exit	Exit the file system
