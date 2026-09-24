Yes. For learning properly, your PowerShell notes should include **Command → What it does → Syntax → Example → Expected result**. Below is a more complete **Basic → Intermediate → Advanced → DevOps** version, including **folder/file create, copy, move, rename, delete, search, permissions, processes, networking, etc.**

# 🪟 PowerShell Complete Roadmap

## 🟢 LEVEL 1 — Basic File & Folder Commands

### 1. `Get-Location` — Show current folder

**Purpose:** Shows which directory you are currently inside.

```powershell
Get-Location
```

Example output:

```text
Path
----
C:\Users\dheen
```

Short command:

```powershell
pwd
```

---

### 2. `Set-Location` — Change folder

**Purpose:** Move from one folder to another.

```powershell
Set-Location C:\Users\dheen\Documents
```

Short form:

```powershell
cd C:\Users\dheen\Documents
```

Go one level back:

```powershell
cd ..
```

Go to home directory:

```powershell
cd ~
```

Go to C drive:

```powershell
cd C:\
```

---

# 📁 3. `Get-ChildItem` — List files and folders

**Purpose:** Shows files and folders inside the current directory.

```powershell
Get-ChildItem
```

Short forms:

```powershell
ls
```

```powershell
dir
```

Example:

```text
Documents
Downloads
Pictures
project
file.txt
```

Show hidden files:

```powershell
Get-ChildItem -Force
```

---

# 📁 4. `New-Item` — Create a folder

**Purpose:** Creates a new file or folder.

Create folder:

```powershell
New-Item -ItemType Directory test
```

Short form:

```powershell
mkdir test
```

Example:

```text
C:\Users\dheen
        ↓
      test
```

Create multiple folders:

```powershell
mkdir frontend, backend, database
```

---

# 📄 5. Create a file

```powershell
New-Item file.txt
```

Better explicit version:

```powershell
New-Item -ItemType File file.txt
```

Create a JavaScript file:

```powershell
New-Item server.js
```

Create a PowerShell script:

```powershell
New-Item script.ps1
```

Create an HTML file:

```powershell
New-Item index.html
```

---

# ✏️ 6. Add content to a file

### `Set-Content`

Creates/replaces file content.

```powershell
Set-Content file.txt "Hello World"
```

Check:

```powershell
Get-Content file.txt
```

Output:

```text
Hello World
```

⚠️ `Set-Content` replaces existing content.

---

# ➕ 7. `Add-Content` — Add content

**Purpose:** Adds new content without removing existing content.

```powershell
Add-Content file.txt "Welcome to PowerShell"
```

Now:

```powershell
Get-Content file.txt
```

Output:

```text
Hello World
Welcome to PowerShell
```

Very useful for logs.

---

# 📖 8. `Get-Content` — Read file

```powershell
Get-Content file.txt
```

Short:

```powershell
cat file.txt
```

Read last 10 lines:

```powershell
Get-Content app.log -Tail 10
```

Follow a log continuously:

```powershell
Get-Content app.log -Wait
```

This is useful for **application/DevOps logs**.

---

# 📋 9. `Copy-Item` — Copy file

```powershell
Copy-Item file.txt backup.txt
```

Copy to another folder:

```powershell
Copy-Item file.txt C:\Temp\
```

Copy folder:

```powershell
Copy-Item project C:\Backup\ -Recurse
```

`-Recurse` means include everything inside the folder.

---

# 🚚 10. `Move-Item` — Move file/folder

```powershell
Move-Item file.txt C:\Temp\
```

Move folder:

```powershell
Move-Item project C:\Backup\
```

Rename using `Move-Item`:

```powershell
Move-Item old.txt new.txt
```

---

# ✏️ 11. `Rename-Item` — Rename

Rename file:

```powershell
Rename-Item file.txt newfile.txt
```

Rename folder:

```powershell
Rename-Item oldfolder newfolder
```

Example:

```text
project
   ↓
my-project
```

```powershell
Rename-Item project my-project
```

---

# 🗑️ 12. `Remove-Item` — Delete file

```powershell
Remove-Item file.txt
```

Delete multiple files:

```powershell
Remove-Item *.log
```

Delete a folder:

```powershell
Remove-Item test -Recurse
```

Force delete:

```powershell
Remove-Item test -Recurse -Force
```

### ⚠️ Important

PowerShell's `Remove-Item` is normally permanent; it does not work like moving something to the Recycle Bin.

---

# 🔍 13. Find files

Find all `.txt` files:

```powershell
Get-ChildItem -Filter "*.txt"
```

Search inside subfolders:

```powershell
Get-ChildItem -Recurse -Filter "*.txt"
```

Find `.log` files:

```powershell
Get-ChildItem -Recurse -Filter "*.log"
```

Find a specific filename:

```powershell
Get-ChildItem -Recurse -Filter "package.json"
```

---

# 🔎 14. Search inside files

### `Select-String`

Find `"error"` inside a log:

```powershell
Select-String "error" app.log
```

Search all log files:

```powershell
Get-ChildItem -Recurse -Filter "*.log" |
Select-String "error"
```

This is similar to Linux `grep`.

---

# 🟢 LEVEL 2 — System Commands

## 15. `hostname`

Shows computer name.

```powershell
hostname
```

---

## 16. `whoami`

Shows current Windows user.

```powershell
whoami
```

Example:

```text
DESKTOP-ABC\dheen
```

---

## 17. PowerShell version

```powershell
$PSVersionTable
```

Only version:

```powershell
$PSVersionTable.PSVersion
```

---

## 18. Windows information

```powershell
Get-ComputerInfo
```

Specific information:

```powershell
Get-ComputerInfo |
Select-Object WindowsProductName, WindowsVersion
```

---

# ⚙️ LEVEL 3 — Processes

## 19. `Get-Process`

Show running applications:

```powershell
Get-Process
```

Find Chrome:

```powershell
Get-Process chrome
```

Find Node:

```powershell
Get-Process node
```

Find Docker:

```powershell
Get-Process *docker*
```

---

## 20. Stop process

```powershell
Stop-Process -Name notepad
```

Force:

```powershell
Stop-Process -Name notepad -Force
```

Example:

If Node.js is stuck:

```powershell
Get-Process node
```

Then:

```powershell
Stop-Process -Name node
```

---

# ⚙️ LEVEL 4 — Windows Services

## 21. List services

```powershell
Get-Service
```

Find a service:

```powershell
Get-Service Spooler
```

---

## 22. Start service

```powershell
Start-Service Spooler
```

---

## 23. Stop service

```powershell
Stop-Service Spooler
```

---

## 24. Restart service

```powershell
Restart-Service Spooler
```

Check:

```powershell
Get-Service Spooler
```

---

# 🌐 LEVEL 5 — Networking

## 25. `ipconfig`

Show IP:

```powershell
ipconfig
```

Detailed:

```powershell
ipconfig /all
```

---

## 26. PowerShell IP command

```powershell
Get-NetIPAddress
```

IPv4 only:

```powershell
Get-NetIPAddress -AddressFamily IPv4
```

---

## 27. Network adapter

```powershell
Get-NetAdapter
```

---

## 28. DNS

```powershell
nslookup google.com
```

PowerShell version:

```powershell
Resolve-DnsName google.com
```

---

## 29. Ping

```powershell
ping google.com
```

PowerShell:

```powershell
Test-Connection google.com
```

---

## 30. Test TCP port ⭐

Very important for DevOps:

```powershell
Test-NetConnection google.com -Port 443
```

Local Node.js:

```powershell
Test-NetConnection localhost -Port 5000
```

EC2 SSH:

```powershell
Test-NetConnection <EC2-IP> -Port 22
```

Example result:

```text
ComputerName     : localhost
RemotePort       : 5000
TcpTestSucceeded : True
```

`True` = port reachable.

---

# 🌐 LEVEL 6 — HTTP/API

## 31. `Invoke-WebRequest`

Check website:

```powershell
Invoke-WebRequest https://google.com
```

Only status code:

```powershell
(Invoke-WebRequest https://google.com).StatusCode
```

Expected:

```text
200
```

---

## 32. `Invoke-RestMethod`

Useful for APIs.

GET:

```powershell
Invoke-RestMethod http://localhost:5000/api/products
```

POST:

```powershell
Invoke-RestMethod `
    -Uri "http://localhost:5000/api/users" `
    -Method POST `
    -ContentType "application/json" `
    -Body '{"name":"Dheena"}'
```

This is useful when testing your **Express/Node.js backend**.

---

# 🌎 LEVEL 7 — Environment Variables

View all:

```powershell
Get-ChildItem Env:
```

View PATH:

```powershell
$env:PATH
```

Create temporary variable:

```powershell
$env:APP_ENV="development"
```

Check:

```powershell
$env:APP_ENV
```

Set permanent user variable:

```powershell
[Environment]::SetEnvironmentVariable(
    "APP_ENV",
    "development",
    "User"
)
```

---

# 🔥 LEVEL 8 — Pipeline

The `|` pipeline is one of the **most important PowerShell concepts**.

```powershell
Get-Process | Where-Object CPU -gt 100
```

Meaning:

```text
Get all processes
       ↓
   filter CPU > 100
       ↓
     result
```

---

# 🔎 LEVEL 9 — Filter / Select / Sort

### `Where-Object`

Filter:

```powershell
Get-Service |
Where-Object Status -eq "Running"
```

---

### `Select-Object`

Show only selected properties:

```powershell
Get-Process |
Select-Object Name, Id, CPU
```

---

### `Sort-Object`

Sort by CPU:

```powershell
Get-Process |
Sort-Object CPU -Descending
```

Combined:

```powershell
Get-Process |
Where-Object CPU -gt 10 |
Sort-Object CPU -Descending |
Select-Object Name, Id, CPU
```

This is an important PowerShell skill.

---

# 💾 LEVEL 10 — Disk & Storage

Show drives:

```powershell
Get-PSDrive
```

Example:

```text
Name Used GB Free GB
C
D
```

Volumes:

```powershell
Get-Volume
```

Physical disks:

```powershell
Get-Disk
```

Partitions:

```powershell
Get-Partition
```

---

# 🧹 LEVEL 11 — Windows Cleanup

### User Temp

```powershell
Remove-Item "$env:LOCALAPPDATA\Temp\*" -Recurse -Force -ErrorAction SilentlyContinue
```

### Windows Temp

```powershell
Remove-Item "C:\Windows\Temp\*" -Recurse -Force -ErrorAction SilentlyContinue
```

### Recycle Bin

```powershell
Clear-RecycleBin -Force
```

### Disk Cleanup

```powershell
cleanmgr
```

Some files will remain because they are currently being used. That's normal.

---

# 👤 LEVEL 12 — Users

List users:

```powershell
Get-LocalUser
```

List groups:

```powershell
Get-LocalGroup
```

Check administrators:

```powershell
Get-LocalGroupMember Administrators
```

Create user:

```powershell
New-LocalUser "devuser"
```

Disable:

```powershell
Disable-LocalUser "devuser"
```

Enable:

```powershell
Enable-LocalUser "devuser"
```

---

# 🔐 LEVEL 13 — Permissions

Check permissions:

```powershell
Get-Acl C:\Users\dheen
```

Detailed:

```powershell
Get-Acl C:\Users\dheen | Format-List
```

For example:

```text
Path
Owner
Access
```

This becomes important for **Windows Server, security and DevOps**.

---

# 🛡️ LEVEL 14 — Firewall

Firewall status:

```powershell
Get-NetFirewallProfile
```

List rules:

```powershell
Get-NetFirewallRule
```

Enabled rules:

```powershell
Get-NetFirewallRule |
Where-Object Enabled -eq "True"
```

For troubleshooting, combine firewall checking with:

```powershell
Test-NetConnection localhost -Port 5000
```

---

# 📜 LEVEL 15 — Event Logs

List logs:

```powershell
Get-WinEvent -ListLog *
```

System logs:

```powershell
Get-WinEvent -LogName System -MaxEvents 20
```

Application logs:

```powershell
Get-WinEvent -LogName Application -MaxEvents 20
```

Find errors:

```powershell
Get-WinEvent -LogName System |
Where-Object LevelDisplayName -eq "Error"
```

---

# ⏰ LEVEL 16 — Scheduled Tasks

List:

```powershell
Get-ScheduledTask
```

Find:

```powershell
Get-ScheduledTask -TaskName "TaskName"
```

Run:

```powershell
Start-ScheduledTask -TaskName "TaskName"
```

---

# 🧠 LEVEL 17 — PowerShell Variables

```powershell
$name = "Dheena"
$age = 20
$port = 5000
```

Display:

```powershell
$name
```

Multiple variables:

```powershell
$app = "MERN"
$frontend = 3000
$backend = 5000

Write-Host "$app frontend: $frontend"
Write-Host "$app backend: $backend"
```

---

# 🔀 LEVEL 18 — Conditions

```powershell
$port = 5000

if ($port -eq 5000) {
    Write-Host "Backend is running"
}
```

Multiple conditions:

```powershell
if ($port -eq 5000) {
    Write-Host "MERN backend"
}
else {
    Write-Host "Different port"
}
```

---

# 🔁 LEVEL 19 — Loops

```powershell
foreach ($process in Get-Process) {
    Write-Host $process.Name
}
```

Example with numbers:

```powershell
foreach ($i in 1..5) {
    Write-Host "Number: $i"
}
```

---

# 🧩 LEVEL 20 — Functions

Create reusable command:

```powershell
function Test-Port {
    param(
        $ComputerName,
        $Port
    )

    Test-NetConnection $ComputerName -Port $Port
}
```

Use:

```powershell
Test-Port localhost 5000
```

Or:

```powershell
Test-Port google.com 443
```

This is where PowerShell starts becoming a real **automation language**, rather than just a command-line tool.

---

# 🔴 LEVEL 21 — Remote Management

Connect:

```powershell
Enter-PSSession SERVER01
```

Run command remotely:

```powershell
Invoke-Command -ComputerName SERVER01 -ScriptBlock {
    Get-Service
}
```

Copy file:

```powershell
Copy-Item file.txt \\SERVER01\C$\Temp\
```

Useful for **Windows Server administration**.

---

# 🚀 LEVEL 22 — DevOps Commands

Once your PowerShell foundation is strong, connect it to your DevOps tools.

### Git

```powershell
git status
git add .
git commit -m "update"
git pull
git push
git log --oneline
git branch
```

### Node.js

```powershell
node -v
npm -v
npm install
npm run dev
npm start
```

### Docker

```powershell
docker --version
docker ps
docker ps -a
docker images
docker pull nginx
docker build -t myapp .
docker run -p 5000:5000 myapp
docker logs <container>
docker exec -it <container> sh
docker stop <container>
docker rm <container>
```

### Kubernetes

```powershell
kubectl get nodes
kubectl get pods
kubectl get deployments
kubectl get services
kubectl describe pod <pod>
kubectl logs <pod>
kubectl exec -it <pod> -- sh
```

### AWS CLI

```powershell
aws --version
aws configure
aws sts get-caller-identity
aws ec2 describe-instances
aws s3 ls
```

---

# ⭐ Your Final Learning Structure

```text
POWER SHELL
│
├── 1. NAVIGATION
│   ├── pwd
│   ├── cd
│   └── Get-Location
│
├── 2. FILE & FOLDER
│   ├── Get-ChildItem
│   ├── New-Item
│   ├── Copy-Item
│   ├── Move-Item
│   ├── Rename-Item
│   └── Remove-Item
│
├── 3. FILE CONTENT
│   ├── Get-Content
│   ├── Set-Content
│   └── Add-Content
│
├── 4. SYSTEM
│   ├── hostname
│   ├── whoami
│   ├── Get-ComputerInfo
│   └── $PSVersionTable
│
├── 5. PROCESS / SERVICE
│   ├── Get-Process
│   ├── Stop-Process
│   ├── Get-Service
│   └── Restart-Service
│
├── 6. NETWORK
│   ├── ipconfig
│   ├── nslookup
│   ├── ping
│   ├── Resolve-DnsName
│   └── Test-NetConnection
│
├── 7. PIPELINE
│   ├── |
│   ├── Where-Object
│   ├── Select-Object
│   └── Sort-Object
│
├── 8. SCRIPTING
│   ├── Variables
│   ├── if / else
│   ├── foreach
│   └── functions
│
├── 9. ADMIN
│   ├── Users
│   ├── Permissions
│   ├── Firewall
│   ├── Event Logs
│   └── Scheduled Tasks
│
└── 10. DEVOPS
    ├── Git
    ├── Node/NPM
    ├── Docker
    ├── Kubernetes
    ├── AWS CLI
    └── CI/CD
```

## 🔥 20 commands to memorize first

```powershell
Get-Location
Set-Location
Get-ChildItem
New-Item
Get-Content
Set-Content
Add-Content
Copy-Item
Move-Item
Rename-Item
Remove-Item
Get-Process
Get-Service
Get-NetIPAddress
Get-NetAdapter
Test-NetConnection
Get-PSDrive
Get-WinEvent
Where-Object
Select-Object
```

**For your MERN + DevOps path**, learn **Levels 1–9 first**, then scripting, and finally use PowerShell to automate **Git → Node → Docker → AWS → Kubernetes → CI/CD**. This gives you a practical Windows DevOps command-line skill set rather than just memorizing commands.
