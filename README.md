Customised Virtual File System (CVFS)

A custom implementation of a Virtual File System built in C/C++.

This project simulates the core functionality of the Linux File System by implementing the kernel-level data structures required for file management. Instead of interacting with the actual hard disk, it maintains a Virtual Disk in Primary Memory (RAM) to simulate file operations, providing a custom shell to interact with the system.

🏗 Technical Architecture

The file system is monolithic and runs entirely in user space. It relies on a specific set of data structures I defined to manage metadata and data allocation, mimicking the Unix File Subsystem.

Key Data Structures Implemented

struct Inode (Linked List): Holds file metadata including File Size, Type (Regular/Special), and Permissions. I implemented this as a Linked List to allow dynamic growth of files.

struct FileTable: Maintains the ReadOffset and WriteOffset context for every open file.

struct SuperBlock: Manages the global state, tracking the total count of available inodes and file system limits.

struct UAREA (User Area): Contains the UFDT (User File Descriptor Table). This is implemented as an array of pointers that maps the integer File Descriptor (FD) to the internal File Table.

Configuration Macros

The system is customizable via the following macros defined in the header:

MAXINODE: Currently set to 50 (Determines the maximum number of files).

MAXFILESIZE: 1024 bytes (Fixed block size per file).

READ/WRITE/EXECUTE: Permission macros mapping to standard integer values (1, 2, and 4).

🛠 Project Features

Custom Shell: A built-in command-line interface to interpret user inputs and execute system calls.

System Call Simulation: Implements the logic for open, close, read, write, and lseek from scratch.

Dynamic Memory Management: Uses malloc and free to allocate Inodes and reclaim memory when files are deleted (unlink).

Error Handling: Custom error codes (-1 to -7) covering scenarios like "Insufficient Space", "File Not Found", or "Permission Denied".

📚 Command Support

The custom shell supports the following commands:

Command

Description

Usage

creat

Create a new file

creat [name] [permission]

write

Write data to file

write [fd]

read

Read data from file

read [fd] [size]

ls

List all files

ls

stat

Show file metadata

stat [name]

unlink

Delete a file

unlink [name]

clear

Clear console

clear

exit

Stop the system

exit

💻 Usage

Compilation

The project combines C-style structural logic with C++ streams. Compile it using g++:

g++ CVFS.cpp -o Myexe


Running the Shell

./Myexe


Example Session

CVFS > help
... displays command list ...

CVFS > creat Notes.txt 3
File created successfully with FD: 0

CVFS > write 0
Enter Data: Hello World
11 bytes written successfully.

CVFS > stat Notes.txt
File Name: Notes.txt
File Size: 1024
Link Count: 1


🔮 Future Enhancements

This is an ongoing project. Future iterations will include:

[ ] Persistence: Saving the Inode and Data blocks to a physical file on disk so data isn't lost on exit.

[ ] Multi-user support: Enhancing the UAREA to support simulated multiple users.

[ ] Directory Support: Implementing hierarchical directories (currently a flat file system).

👤 Author

Rohan Murlidhar Pawar

LinkedIn

GitHub
