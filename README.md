🚀 Customised Virtual File System (CVFS)
A custom implementation of a Virtual File System built in C/C++.
This project simulates the core functionality of the Linux File System by implementing the kernel-level data structures required for file management. Instead of interacting with the actual hard disk, it maintains a Virtual Disk in RAM, providing a custom shell to interact with the system.
🏗️ Technical Architecture
The file system is monolithic and runs entirely in user space. It relies on internally defined data structures to manage metadata and data allocation, mimicking the Unix File Subsystem.
🔑 Key Data Structures Implemented
📌 struct Inode (Linked List)
Holds file metadata: File Size, Type (Regular/Special), Permissions
Implemented as a Linked List to support dynamic file creation
📌 struct FileTable
Maintains:
ReadOffset
WriteOffset
Stores runtime context for every open file
📌 struct SuperBlock
Manages global file system state:
Total inode count
Free inode count
File system limits
📌 struct UAREA (User Area)
Contains the UFDT (User File Descriptor Table)
Maps File Descriptors (FD) → internal FileTable pointers
⚙️ Configuration Macros
Macro	Value	Description
MAXINODE	50	Maximum number of files
MAXFILESIZE	1024 bytes	Fixed block size per file
READ / WRITE / EXECUTE	1 / 2 / 4	Standard permission macros
🛠️ Project Features
✔️ Custom Shell
A built-in command-line interface to interpret user inputs and execute system calls.
✔️ System Call Simulation
Implements custom logic for:
open, close, read, write, lseek
✔️ Dynamic Memory Management
Uses malloc and free to allocate inodes and reclaim memory on file deletion.
✔️ Error Handling
Custom error codes (-1 to -7) for:
Insufficient Space
File Not Found
Permission Denied
Invalid Operation
📚 Command Support
Command	Description	Usage
creat	Create a new file	creat [name] [permission]
write	Write data to a file	write [fd]
read	Read data from a file	read [fd] [size]
ls	List all files	ls
stat	Show file metadata	stat [name]
unlink	Delete a file	unlink [name]
clear	Clear console	clear
exit	Exit the system	exit
💻 Usage
🧪 Compilation
g++ CVFS.cpp -o Myexe
▶️ Running the Shell
./Myexe
📝 Example Session
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
 Persistence: Save inodes and data blocks to physical disk
 Multi-user support: Enhance UAREA for multiple user environments
 Directory Support: Add hierarchical directory structure
👤 Author
Rohan Murlidhar Pawar
🔗 LinkedIn
🔗 GitHub
