# Linux Learning Notes 🐧

A collection of Linux commands, concepts, and practical examples learned while studying Linux. These notes cover basic terminal navigation, file management, users and groups, permissions, package management, processes, services, environment variables, archiving, compression, and cron jobs.

The purpose of this repository is to maintain simple, beginner-friendly Linux notes for revision and practical learning.

---

## 📑 Table of Contents

1. [Basic Linux Commands](#1-basic-linux-commands)
2. [Linux Directory Structure](#2-linux-directory-structure)
3. [File and Directory Management](#3-file-and-directory-management)
4. [Viewing File Contents](#4-viewing-file-contents)
5. [Users and Groups](#5-users-and-groups)
6. [File Permissions and Ownership](#6-file-permissions-and-ownership)
7. [Package Management](#7-package-management)
8. [Processes and Process Management](#8-processes-and-process-management)
9. [System Services](#9-system-services)
10. [Environment Variables and PATH](#10-environment-variables-and-path)
11. [Configuration Files](#11-configuration-files)
12. [Archiving and Compression](#12-archiving-and-compression)
13. [Cron Jobs and Task Scheduling](#13-cron-jobs-and-task-scheduling)
14. [SSH (Secure Shell)](#14-SSH-(secure-shell))

---

# 1. Basic Linux Commands

These commands help us interact with the Linux terminal and navigate the system.

| Command | Description |
|---|---|
| `pwd` | Displays the current working directory. |
| `cd` | Changes the current directory. |
| `ls` | Lists files and directories. |
| `clear` | Clears the terminal screen. |
| `history` | Displays previously executed commands. |

### 1.1 pwd – Print Working Directory

Displays the path of the directory we are currently working in.

```bash
pwd
```

### 1.2 cd – Change Directory

Used to move from one directory to another.

```bash
cd Documents
```

Move to the home directory:

```bash
cd ~
```

### 1.3 ls – List Files

Displays files and directories in the current directory.

```bash
ls
```

### 1.4 Tab Autocomplete

The `Tab` key automatically completes commands, file names, and directory names when possible.

Example:

```bash
cd Doc<Tab>
```

The terminal may automatically complete it to:

```bash
cd Documents
```

### 1.5 clear

Clears the terminal screen.

```bash
clear
```

### 1.6 history

Displays the commands previously executed in the terminal.

```bash
history
```

---

# 2. Linux Directory Structure

Linux uses a hierarchical directory structure that starts from the root directory.

### Important Directories and Symbols

| Directory / Symbol | Description |
|---|---|
| `/` | Root directory. The starting point of the Linux filesystem. |
| `/etc` | Contains system-wide configuration files. |
| `/usr` | Contains many user-space programs, libraries, and shared resources. |
| `/tmp` | Stores temporary files. |
| `~` | Represents the current user's home directory. |
| `~/.bashrc` | Hidden configuration file in the user's home directory. |

### Examples

Go to the root directory:

```bash
cd /
```

Go to the home directory:

```bash
cd ~
```

Access the `/etc` directory:

```bash
cd /etc
```

Access the temporary directory:

```bash
cd /tmp
```

---

# 3. File and Directory Management

Linux provides commands to create, copy, and delete files and directories.

### 3.1 mkdir – Make Directory

Creates a new directory.

```bash
mkdir folder_name
```

Example:

```bash
mkdir Linux
```

### 3.2 mkdir -p

Creates parent directories along with the specified directory if they do not already exist.

```bash
mkdir -p parent/child/folder
```

### 3.3 touch

Creates an empty file if it does not exist.

```bash
touch filename.txt
```

Example:

```bash
touch notes.txt
```

It can also update the timestamp of an existing file.

### 3.4 cp – Copy

Copies files or directories from one location to another.

**Syntax:**

```bash
cp source destination
```

Example:

```bash
cp file.txt backup.txt
```

Copy a file into another directory:

```bash
cp file.txt Documents/
```

### 3.5 rm – Remove

Deletes a file.

```bash
rm filename
```

Example:

```bash
rm notes.txt
```

### 3.6 rm -rf

Deletes a directory and all its contents recursively and forcefully.

```bash
rm -rf directory_name
```

| Option | Meaning |
|---|---|
| `-r` | Recursive deletion. Deletes directories and their contents. |
| `-f` | Force deletion without prompting. |

**Important:** Be careful with `rm -rf`. Deleted files are generally not moved to the recycle bin.

---

# 4. Viewing File Contents

These commands help us read and search information inside files.

### 4.1 cat – Concatenate

Displays the contents of a file.

```bash
cat filename.txt
```

### 4.2 cat -n

Displays file contents with line numbers.

```bash
cat -n filename.txt
```

### 4.3 less

Displays file contents one page at a time.

```bash
less filename.txt
```

Useful keys inside `less`:

| Key | Description |
|---|---|
| `/word` | Searches for a word or pattern. |
| `n` | Moves to the next search match. |
| `q` | Exits `less`. |

### Difference Between cat and less

| cat | less |
|---|---|
| Displays the file contents directly. | Displays contents one page at a time. |
| Suitable for smaller files. | Useful for larger files. |
| Does not provide interactive page navigation. | Supports scrolling and searching. |

---

# 5. Users and Groups

Linux is a multi-user operating system. Users and groups help manage access and permissions.

### 5.1 sudo

Runs a command with administrative privileges, if the user is authorized.

Example:

```bash
sudo apt update
```

### 5.2 adduser

Creates a new user account.

```bash
sudo adduser username
```

Example:

```bash
sudo adduser rahul
```

This command interactively asks for details such as a password and user information.

### 5.3 useradd

Creates a new user account.

```bash
sudo useradd -m username
```

The `-m` option creates a home directory for the new user.

### 5.4 su

Switches to another user account.

```bash
su - username
```

The `-` option starts a login shell and loads the target user's login environment.

### 5.5 usermod

Modifies an existing user account.

Add a user to an additional group:

```bash
sudo usermod -aG groupname username
```

Example:

```bash
sudo usermod -aG developers rahul
```

**Important options:**

| Option | Meaning |
|---|---|
| `-a` | Append the user to additional groups. |
| `-G` | Specify supplementary groups. |

### 5.6 Giving a User sudo Privileges

To give a user administrative privileges, add the user to the `sudo` group.

```bash
sudo usermod -aG sudo username
```

Example:

```bash
sudo usermod -aG sudo rahul
```

The user may need to log out and log in again for the new group membership to take effect.

### 5.7 groups

Displays the groups to which a user belongs.

```bash
groups username
```

Example:

```bash
groups rahul
```

### 5.8 userdel

Deletes a user account.

```bash
sudo userdel username
```

---

# 6. File Permissions and Ownership

Linux uses permissions to control who can read, write, and execute files.

There are three main permission categories:

| Symbol | Meaning |
|---|---|
| `u` | User / Owner |
| `g` | Group |
| `o` | Others |
| `a` | All (user, group, and others) |

### 6.1 Permission Types

| Symbol | Permission | Meaning |
|---|---|---|
| `r` | Read | Allows reading a file. |
| `w` | Write | Allows modifying a file. |
| `x` | Execute | Allows executing a file or entering a directory. |

### 6.2 chmod – Change Mode

Changes file or directory permissions.

**Syntax:**

```bash
chmod permissions filename
```

Example:

```bash
chmod u+rwx,g+rx,o+r filename
```

Explanation:

- `u+rwx`: Gives the owner read, write, and execute permissions.
- `g+rx`: Gives the group read and execute permissions.
- `o+r`: Gives others read permission.

### 6.3 chmod +x

Adds execute permission to a file.

```bash
chmod +x filename
```

Example:

```bash
chmod +x script.sh
```

Now the script can be executed using:

```bash
./script.sh
```

### 6.4 Numeric Permissions

Linux also supports numeric permissions.

| Number | Permission |
|---|---|
| `4` | Read (`r`) |
| `2` | Write (`w`) |
| `1` | Execute (`x`) |
| `7` | Read + Write + Execute (`rwx`) |
| `6` | Read + Write (`rw-`) |
| `5` | Read + Execute (`r-x`) |
| `0` | No permissions (`---`) |

Example:

```bash
chmod 755 filename
```

Explanation:

- Owner: `7` = Read, Write, Execute.
- Group: `5` = Read, Execute.
- Others: `5` = Read, Execute.

### 6.5 groupadd

Creates a new group.

```bash
sudo groupadd groupname
```

Example:

```bash
sudo groupadd developers
```

### 6.6 chown – Change Owner

Changes the owner and group of a file or directory.

```bash
sudo chown username:groupname filename
```

Example:

```bash
sudo chown rahul:developers file.txt
```

### 6.7 chgrp – Change Group

Changes the group ownership of a file or directory.

```bash
sudo chgrp groupname filename
```

Example:

```bash
sudo chgrp developers file.txt
```

### Difference Between chmod, chown, and chgrp

| Command | Purpose |
|---|---|
| `chmod` | Changes file permissions. |
| `chown` | Changes file owner and optionally group. |
| `chgrp` | Changes file group ownership. |

---

# 7. Package Management

Ubuntu and other Debian-based Linux distributions use the APT package manager to install, update, and remove software.

### 7.1 apt update

Updates the package lists from configured software repositories.

```bash
sudo apt update
```

### 7.2 apt upgrade

Upgrades installed packages to newer available versions.

```bash
sudo apt upgrade
```

### 7.3 apt install

Installs a package.

```bash
sudo apt install package_name
```

Example:

```bash
sudo apt install nginx
```

### 7.4 apt show

Displays detailed information about a package.

```bash
apt show package_name
```

Example:

```bash
apt show nginx
```

### 7.5 apt purge

Removes a package along with its system-wide package configuration files.

```bash
sudo apt purge package_name
```

Example:

```bash
sudo apt purge nginx
```

### 7.6 apt list --installed

Displays installed packages.

```bash
apt list --installed
```

### Difference Between apt update and apt upgrade

| Command | Purpose |
|---|---|
| `sudo apt update` | Refreshes the package information from repositories. |
| `sudo apt upgrade` | Installs available upgrades for installed packages. |

---

# 8. Processes and Process Management

A process is a running instance of a program.

Linux provides commands to view, monitor, and manage running processes.

### 8.1 ps

Displays information about currently running processes.

```bash
ps
```

### 8.2 ps aux

Displays detailed information about processes running on the system.

```bash
ps aux
```

### 8.3 grep

Searches for specific text or patterns in files or command output.

```bash
grep "word" filename
```

Example:

```bash
grep "error" log.txt
```

### 8.4 Pipe Operator ( | )

The pipe operator passes the output of one command as input to another command.

Example:

```bash
ps aux | grep nginx
```

Explanation:

1. `ps aux` displays running processes.
2. `|` passes the output to the next command.
3. `grep nginx` searches for processes containing `nginx`.

### 8.5 top

Displays real-time information about running processes, CPU usage, and memory usage.

```bash
top
```

### 8.6 htop

An interactive process-monitoring tool that displays CPU usage, memory usage, and running processes.

```bash
htop
```

**Note:** If `htop` is not installed, install it using:

```bash
sudo apt install htop
```

Inside `htop`:

- Press `F6` to open the sorting menu.
- You can sort processes by CPU usage, memory usage, PID, and other fields.

### 8.7 kill

Sends a termination signal to a process using its Process ID (PID).

```bash
kill PID
```

Example:

```bash
kill 1234
```

### 8.8 kill -9

Forcefully terminates a process using the SIGKILL signal.

```bash
kill -9 PID
```

Example:

```bash
kill -9 1234
```

**Difference:**

| Command | Description |
|---|---|
| `kill PID` | Normally sends SIGTERM, allowing the process to shut down gracefully. |
| `kill -9 PID` | Sends SIGKILL and forcefully terminates the process. |

---

# 9. System Services

Linux services are background programs that provide system functionality.

The `systemctl` command is used to manage services on systems that use systemd.

### 9.1 Check Service Status

```bash
systemctl status service_name
```

Example:

```bash
systemctl status cron
```

### 9.2 Start a Service

Starts a service.

```bash
sudo systemctl start service_name
```

Example:

```bash
sudo systemctl start cron
```

### 9.3 Stop a Service

Stops a running service.

```bash
sudo systemctl stop service_name
```

Example:

```bash
sudo systemctl stop cron
```

### 9.4 Restart a Service

Stops and starts a service again.

```bash
sudo systemctl restart service_name
```

Example:

```bash
sudo systemctl restart cron
```

### 9.5 Reload a Service

Reloads a service's configuration without fully restarting it, if the service supports reloading.

```bash
sudo systemctl reload service_name
```

### 9.6 Enable a Service

Configures a service to start automatically during system boot.

```bash
sudo systemctl enable service_name
```

### 9.7 Disable a Service

Prevents a service from starting automatically during system boot.

```bash
sudo systemctl disable service_name
```

### Important systemctl Commands

| Command | Purpose |
|---|---|
| `start` | Starts a service now. |
| `stop` | Stops a service now. |
| `restart` | Restarts a service. |
| `reload` | Reloads configuration, if supported. |
| `status` | Checks service status. |
| `enable` | Enables automatic startup at boot. |
| `disable` | Disables automatic startup at boot. |

**Important:** `start` and `enable` are different. Starting a service does not automatically configure it to start at boot.

---

# 10. Environment Variables and PATH

Environment variables store information that can be accessed by programs and processes.

### 10.1 echo

Displays text or the value of an environment variable.

```bash
echo "Hello Linux"
```

Display an environment variable:

```bash
echo $HOME
```

### 10.2 printenv

Displays environment variables.

```bash
printenv
```

Display a specific environment variable:

```bash
printenv HOME
```

### 10.3 export

Creates or sets an environment variable for the current shell and its child processes.

**Syntax:**

```bash
export VARIABLE_NAME=value
```

Example:

```bash
export NAME=Rahul
```

Access its value:

```bash
echo $NAME
```

**Note:** Variables created using `export` in the current shell are generally temporary and do not automatically persist after closing the terminal.

### 10.4 which

Displays the location of an executable command.

```bash
which command_name
```

Example:

```bash
which python3
```

It may return something like:

```text
/usr/bin/python3
```

### 10.5 PATH

`PATH` is an environment variable containing directories where Linux searches for executable commands.

Display its value:

```bash
echo $PATH
```

### 10.6 Execute a File Using ./

The `./` notation executes a file from the current directory.

```bash
./filename
```

Example:

```bash
./script.sh
```

The file must have execute permission.

If necessary, provide execute permission:

```bash
chmod +x script.sh
```

---

# 11. Configuration Files

Configuration files store settings used by Linux programs and the shell.

### 11.1 /etc

The `/etc` directory contains system-wide configuration files.

```bash
cd /etc
```

### 11.2 ~/.bashrc

The `.bashrc` file is a hidden configuration file located in the user's home directory.

It is commonly used to store:

- Shell aliases.
- Environment variables.
- Shell customization.
- Other Bash settings.

Open the file:

```bash
vim ~/.bashrc
```

### 11.3 source

Runs commands from a file in the current shell.

```bash
source filename
```

Example:

```bash
source ~/.bashrc
```

This is useful when you modify `.bashrc` and want the changes to take effect without opening a new terminal.

### 11.4 vim – Text Editor

`vim` is a terminal-based text editor used to create and edit files.

Open a file:

```bash
vim filename
```

Important Vim commands:

| Key / Command | Description |
|---|---|
| `i` | Enters Insert mode to type or edit text. |
| `Esc` | Exits Insert mode. |
| `:wq` | Saves changes and quits Vim. |

Example workflow:

1. Open a file:

   ```bash
   vim notes.txt
   ```

2. Press `i` to enter Insert mode.
3. Type or edit the content.
4. Press `Esc`.
5. Type `:wq` and press Enter to save and exit.

---

# 12. Archiving and Compression

Archiving combines files and directories into a single archive. Compression reduces file size.

Linux provides commands such as `tar`, `gzip`, `zip`, and `unzip`.

## 12.1 tar – Tape Archive

The `tar` command is used to create, list, and extract archive files.

### Create an Archive: tar -cf

```bash
tar -cf archive.tar filename
```

Creates a `.tar` archive containing the specified file or directory.

| Option | Meaning |
|---|---|
| `c` | Create a new archive. |
| `f` | Specify the archive filename. |

Example:

```bash
tar -cf backup.tar Documents
```

### List Archive Contents: tar -tf

```bash
tar -tf archive.tar
```

Lists the contents of an archive without extracting it.

| Option | Meaning |
|---|---|
| `t` | List archive contents. |
| `f` | Specify the archive filename. |

Example:

```bash
tar -tf backup.tar
```

### Extract an Archive: tar -xf

```bash
tar -xf archive.tar
```

Extracts files from an archive into the current directory.

| Option | Meaning |
|---|---|
| `x` | Extract files. |
| `f` | Specify the archive filename. |

Example:

```bash
tar -xf backup.tar
```

### Extract with Verbose Output: tar -xvf

```bash
tar -xvf archive.tar
```

Extracts files and displays the names of files being extracted.

| Option | Meaning |
|---|---|
| `x` | Extract files. |
| `v` | Verbose; display file names. |
| `f` | Specify the archive filename. |

Example:

```bash
tar -xvf backup.tar
```

## 12.2 gzip

`gzip` compresses files and creates `.gz` files.

### Compress a File

```bash
gzip filename
```

Example:

```bash
gzip notes.txt
```

This creates:

```text
notes.txt.gz
```

The original file is normally replaced by the compressed file.

### Decompress a File: gunzip

```bash
gunzip filename.gz
```

Example:

```bash
gunzip notes.txt.gz
```

Restores the original file.

## 12.3 zip -r

The `zip` command creates ZIP archives.

Use `-r` to include directories and all their contents recursively.

```bash
zip -r archive.zip directory_name
```

Example:

```bash
zip -r backup.zip Documents
```

| Option | Meaning |
|---|---|
| `r` | Recursive; include all files and subdirectories. |

## 12.4 unzip -l

Lists the contents of a ZIP archive without extracting them.

```bash
unzip -l archive.zip
```

| Option | Meaning |
|---|---|
| `l` | List archive contents. |

Example:

```bash
unzip -l backup.zip
```

To extract a ZIP archive:

```bash
unzip backup.zip
```

### Difference Between Archiving and Compression

| Operation | Command | Purpose |
|---|---|---|
| Create TAR archive | `tar -cf` | Combines files into an archive. |
| List TAR contents | `tar -tf` | Lists archive contents. |
| Extract TAR archive | `tar -xf` | Extracts archive contents. |
| Extract with details | `tar -xvf` | Extracts and displays file names. |
| Compress file | `gzip` | Compresses a file into `.gz`. |
| Decompress file | `gunzip` | Restores a `.gz` file. |
| Create ZIP archive | `zip -r` | Compresses files/directories into ZIP format. |
| List ZIP contents | `unzip -l` | Lists ZIP contents without extracting. |
| Extract ZIP archive | `unzip` | Extracts ZIP contents. |

**Important:** A `.tar` archive combines files but does not necessarily compress them. A `.gz` file uses compression. ZIP combines archiving and compression.

---

# 13. Cron Jobs and Task Scheduling

Cron is a Linux utility used to schedule commands or scripts to run automatically at specific times.

A cron job can automate repetitive tasks without manually running commands.

## 13.1 crontab -l

Displays the cron jobs scheduled for the current user.

```bash
crontab -l
```

| Option | Meaning |
|---|---|
| `-l` | List scheduled cron jobs. |

## 13.2 crontab -e

Opens the current user's crontab file for editing.

```bash
crontab -e
```

Use this command to create, edit, or schedule cron jobs.

## 13.3 Managing the Cron Service

The `systemctl` command can be used to manage the cron service.

### Start Cron

```bash
sudo systemctl start cron
```

Starts the cron service.

### Stop Cron

```bash
sudo systemctl stop cron
```

Stops the cron service.

### Check Cron Status

```bash
sudo systemctl status cron
```

Checks whether the cron service is running.

---

# 14. SSH (Secure Shell)

SSH (Secure Shell) is a protocol used to securely connect to remote computers and servers.

## 14.1 ssh-keygen

Generates a pair of SSH keys (public and private keys).

    ssh-keygen

## 14.2 Generate an RSA SSH Key

Generates an RSA SSH key pair with a key size of 4096 bits.

    ssh-keygen -t rsa -b 4096

- `-t rsa` — Specifies the RSA key type.
- `-b 4096` — Sets the key size to 4096 bits.

**Important:**
- Private key: Keep it secret. Never share it.
- Public key: Can be shared with GitHub or remote servers.

## 14.3 Append Operator (`>>`)

The `>>` operator appends content to the end of a file without overwriting existing content.

    echo "New SSH key" >> ~/.ssh/authorized_keys

**Difference:**
- `>` — Overwrites existing file content.
- `>>` — Appends content while preserving existing data.

## 14.4 Restart SSH Service

Restarts the SSH service.

    sudo service ssh restart

## 14.5 ssh-copy-id

Copies your public SSH key to a remote server for key-based authentication.

**Syntax:**

    ssh-copy-id username@remote_ip

Example:

    ssh-copy-id rahul@192.168.1.100

It usually asks for the remote user's password during the initial setup.

After successful setup, you can connect using your SSH key without entering the account password each time.

## 14.6 Install ssh-copy-id Using Homebrew

Installs the `ssh-copy-id` utility using Homebrew on macOS.

    brew install ssh-copy-id

**Note:** Homebrew  commonly used on macOS.





---
