# 🚀 **Customised Virtual File System (CVFS)**

A custom implementation of a Virtual File System built in **C/C++**.

This project simulates the core functionality of the Linux File System by implementing the kernel-level data structures required for file management. Instead of interacting with the actual hard disk, it maintains a **Virtual Disk in RAM**, providing a **custom shell** to interact with the system.

---

## 🏗️ **Technical Architecture**

The file system is **monolithic** and operates entirely in **user space**. It relies on a set of custom data structures that manage metadata and data allocation, closely mimicking the Unix File Subsystem.

---

## 🔑 **Key Data Structures Implemented**

### 📌 **`struct Inode` (Linked List)**

Holds file metadata including File Size, Type (Regular/Special), and Permissions.
Implemented as a **Linked List** to allow dynamic growth of files.

### 📌 **`struct FileTable`**

Maintains the runtime context for open files:

* ReadOffset
* WriteOffset
* Mode

### 📌 **`struct SuperBlock`**

Tracks the global state of the file system:

* Total inode capacity
* Available inodes
* File system limits

### 📌 **`struct UAREA` (User Area)**

Contains the **UFDT** (User File Descriptor Table).
Maps integer File Descriptors (FD) to internal FileTable structures.

---

## ⚙️ **Configuration Macros**

* **MAXINODE:** 50
  Determines the maximum number of files.

* **MAXFILESIZE:** 1024 bytes
  Fixed block size per file.

* **READ / WRITE / EXECUTE:** 1 / 2 / 4
  Standard permission macros representing read, write, and execute access.

---

## 🛠️ **Project Features**

* **Custom Shell:**
  A built-in command-line interface to interpret user commands and execute system calls.

* **System Call Simulation:**
  Implements the logic of `open`, `close`, `read`, `write`, and `lseek` manually.

* **Dynamic Memory Management:**
  Uses `malloc` and `free` to allocate and release inodes and data memory when files are deleted.

* **Error Handling:**
  Includes custom error codes (-1 to -7) for conditions like:

  * Insufficient space
  * File not found
  * Permission denied

---

## 📚 **Command Support**

**creat** — Create a new file
Usage: `creat [name] [permission]`

**write** — Write data to a file
Usage: `write [fd]`

**read** — Read data from a file
Usage: `read [fd] [size]`

**ls** — List all files
Usage: `ls`

**stat** — Display file metadata
Usage: `stat [name]`

**unlink** — Delete a file
Usage: `unlink [name]`

**clear** — Clear the console
Usage: `clear`

**exit** — Terminate the virtual file system
Usage: `exit`

---

## 💻 **Usage**

### 📦 **Compilation**

```bash
g++ CVFS.cpp -o Myexe
```

### ▶️ **Run the Shell**

```bash
./Myexe
```

---

## 📝 **Example Session**

```
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
```

---

## 🔮 **Future Enhancements**

* [ ] **Persistence:** Store inodes and data blocks on a physical file to prevent data loss.
* [ ] **Multi-user Support:** Extend UAREA to manage multiple simulated users.
* [ ] **Directory Support:** Add hierarchical directory structures instead of the current flat file system.

---

<img width="1132" height="677" alt="CVFS" src="https://github.com/user-attachments/assets/8bb5b3db-4ef6-4711-8beb-ae7be68d6007" />

## 👤 **Author**


**Rohan Murlidhar Pawar**
