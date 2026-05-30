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


**<h4>🛠️ Hands-On Exercise<br></h4>**
1️⃣ Download and open Process Explorer (Sysinternals).

2️⃣ Expand the process tree and locate explorer.exe.

Identify its parent process

Check the user context

Review loaded DLLs

3️⃣ Locate lsass.exe and observe that it runs as a protected system process.

**<h2> Task 2: Investigate Windows File System Structure (NTFS)</h2>** 

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

**<h4>🛠️ Hands-On Exercise</h4><br>**
1️⃣ Open File Explorer and navigate to:

C:\Windows\System32
C:\Users\<YourUser>\AppData

2️⃣ Enable Hidden Items to reveal system folders.

3️⃣ Right-click System32 → Properties → Security.

Identify the owner

Identify which groups have write access

4️⃣ Search for executable files using:

*.exe



**<h2>Task 3: Manage Users, Groups & Privileges</h2>** 

**<h4>🎯 Goal</h4><br>**
Understand how Windows controls access and enforces privileges using users and groups.

**<h4>🔍 Explanation</h4><br>**
Windows is a multi-user operating system. Permissions are assigned through user accounts and group memberships.

User types include:

Administrator → Full system control
Standard User → Limited privileges
System Accounts → Used by services (SYSTEM, LOCAL SERVICE)
Security teams monitor user activity to detect unauthorized access and privilege escalation.

**<h4>🛠️ Hands-On Exercise</h4><br>**
List all users:

netuser

View user details:

net user <username>

List groups:

net localgroup

Check your privileges:

whoami /groups

Create a new user:

netuser student123 Pass@123/add

Add user to Administrators:

net localgroup administrators student123 /add

Log in as the new user and attempt a software installation.



**<h2>Task 4: Analyze Running Processes and Resource Usage</h2>**

**<h4>🎯 Goal</h4><br>**
Understand how Windows executes programs and allocates system resources.

🔍 Explanation</h4><br>**
A process is a running instance of a program. Each process consumes:

CPU
Memory
Disk I/O
Network resources
Windows uses helper processes such as:

svchost.exe to host multiple services
dllhost.exe for COM objects
csrss.exe for critical system operations
Abnormal process behavior is a key indicator in SOC investigations.

**<h4>🛠️ Hands-On Exercise</h4><br>**
1️⃣ Open Task Manager → Processes.

Identify the top 5 CPU-consuming processes

Identify the top 5 memory-consuming processes

2️⃣ Open Resource Monitor and observe disk and network activity.

3️⃣ Launch Notepad and terminate it using Task Manager.

**<h2>Task 5: Inspect and Control Windows Services</h2>**

**<h4>🎯 Goal</h4><br>**
Understand how Windows automates background system functions using services.

**<h4>🔍 Explanation</h4><br>**
A Windows service is a background process that supports core OS functionality.

Services can start:

Automatically
Manually
Be disabled
Improperly configured services can affect performance and security.

**<h4>🛠️ Hands-On Exercise</h4><br>**
1️⃣ Open:

services.msc

2️⃣ Locate:

Windows Update

Windows Defender Antivirus

DHCP Client

3️⃣ Record:

Startup type

Status

Description

4️⃣ Stop and restart a non-critical service (e.g., Print Spooler).

**<h2>Task 6: Explore Windows Registry and Startup Entries</h2>**

**<h4>🎯 Goal</h4><br>**
Understand how Windows stores configuration data and controls startup behavior.

**<h4>🔍 Explanation</h4><br>**
The Windows Registry is a centralized database storing:

OS configuration
Application settings
User preferences
Startup programs
Important registry hives:

HKLM → System-wide settings
HKCU → User-specific settings
HKCR → File associations
Malware often uses registry keys for persistence.

**<h4>🛠️ Hands-On Exercise</h4><br>**
1️⃣ Open Registry Editor:

regedit

2️⃣ Navigate to:

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run

3️⃣ Review startup entries.

4️⃣ Create a temporary string value named TestEntry and delete it.

**<h2>Task 7: Examine Windows Networking Configuration</h2>**

**<h4>🎯 Goal</h4><br>**
Understand how Windows communicates over a network.

**<h4>🔍 Explanation</h4><br>**
Windows networking relies on:

IP addressing
DNS resolution
Routing tables
ARP mappings
These details are essential during troubleshooting and incident response.

**<h4>🛠️ Hands-On Exercise</h4><br>**
Run:

ipconfig /all
arp -a
netstat -ano
routeprint

1️⃣ Identify your IPv4 address

2️⃣ Identify DNS servers

3️⃣ Review active network connections

4️⃣ Identify the process listening on port 80 or 443

**<h2>Task 8: Perform Basic Administration Using PowerShell</h2>**

**<h4>🎯 Goal</h4><br>**
Build foundational scripting and automation skills using PowerShell.

**<h4>🔍 Explanation</h4><br>**
PowerShell is an object-based shell designed for automation and administration.

It is widely used by administrators and frequently abused by attackers.

**<h4>🛠️ Hands-On Exercise</h4><br>**
Run:

Get-Process
Get-Service
Get-LocalUser
Get-EventLog-LogNameSystem-Newest20

Filter services:

Get-Service | ? {$_.Name-like"Win*"}

Export process data:

Get-Process |Export-Csv processes.csv

**<h2>Task 9: Investigate Windows Event Logs</h2>**

**<h4>🎯 Goal</h4><br>**
Understand Windows auditing and authentication trails.

**<h4>🔍 Explanation</h4><br>**
Windows records all security-relevant events, including:

Logins and logouts
Process creation
System failures
Security alerts
Key Event IDs:

4624 → Successful login
4625 → Failed login
4688 → Process creation
1102 → Logs cleared
**<h4>🛠️ Hands-On Exercise</h4><br>**
1️⃣ Open:

eventvwr.msc

2️⃣ Navigate to Security Logs

3️⃣ Filter Event ID 4624

4️⃣ Identify:

Username
Logon type
Source IP (if remote)
Task 10: Review Built-In Windows Security Controls

**<h4>🎯 Goal</h4><br>**
Understand how Windows protects endpoints by default.

**<h4>🔍 Explanation</h4><br>**
Windows includes built-in security mechanisms such as:

Microsoft Defender Antivirus
Windows Firewall
User Account Control (UAC)
BitLocker disk encryption
Account lockout policies
These controls form the foundation of endpoint security.

**<h4>🛠️ Hands-On Exercise</h4><br>**
1️⃣ Open Windows Defender and run a Quick Scan.

2️⃣ Open firewall management:

wf.msc

3️⃣ Open Local Security Policy:

secpol.msc

