**<h1># Windows-Fundamentals</h1>**

**<h2>Task 1: Explore Windows Architecture Using Running Processes <br></h1>**

**<h4>🎯 Goal <br></h4>**
Understand how Windows boots, runs applications, and protects critical system components using user mode and kernel mode separation.

**<h4>🔍 Explanation<br></h4>**
Windows is designed with a layered architecture to ensure stability and security.

User Mode is where applications such as browsers, editors, and desktop programs run. If an application crashes in user mode, it does not crash the entire operating system.
Kernel Mode is the core of Windows. It manages CPU scheduling, memory management, hardware drivers, and security enforcement. Any failure here results in a Blue Screen of Death (BSOD).
Windows depends on several critical background processes:

Explorer.exe manages the desktop, Start Menu, and File Explorer.
LSASS.exe handles authentication and password validation.
CSRSS.exe manages console windows and critical user-mode operations.
Win32 Subsystem acts as the interface between applications and the OS.
Understanding these components is essential for troubleshooting and security investigations.


<h4>**🛠️ Hands-On Exercise**<br></h4>
1️⃣ Download and open Process Explorer (Sysinternals).

2️⃣ Expand the process tree and locate explorer.exe.

Identify its parent process

Check the user context

Review loaded DLLs

3️⃣ Locate lsass.exe and observe that it runs as a protected system process.

<h4> **Task 2: Investigate Windows File System Structure (NTFS)** </h4>

**<h4>🎯 Goal</h4><br>**
Understand Windows directory layout, NTFS features, and permission boundaries.

**<h4>🔍 Explanation</h4><br>**
Windows uses NTFS (New Technology File System), which provides:

File permissions using Access Control Lists (ACLs)
Encryption (EFS)
Compression
Journaling for crash recovery
Important directories include:

C:\Windows\System32 → Core operating system binaries
C:\Program Files → Installed applications
C:\Users → User profiles
AppData → Application configurations, cache, and tokens (critical for forensics)
Both attackers and defenders rely heavily on file system knowledge.
