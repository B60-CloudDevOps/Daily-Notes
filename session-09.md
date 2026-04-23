
***

# Linux Basics – User & Process Management

## Agenda
1. User Management  
2. Service Management  
3. Permissions of Files & Folders  
4. Ownership of Files & Folders  

***

## System Load and Uptime

```bash
$ uptime
01:14:36 up 1 min, 1 user, load average: 0.61, 0.31, 0.12
```

**Load Average** represents the average system load over time.

- Unlike Windows (which shows CPU usage as a percentage), Linux load average shows:
  - Processes actively using CPU
  - Processes waiting for CPU/resources

**Values Explained:**
- First value → Last 1 minute  
- Second value → Last 5 minutes  
- Third value → Last 15 minutes  

***

## Process Management

### `top`
Displays real-time process information and resource usage (refreshes every 3 seconds).

### Process Basics
- Every process has a **PID (Process ID)**  
- Every process has a **PPID (Parent Process ID)**  

### Commands

```bash
sleep 1000
```
Pauses execution for a specified number of seconds.

```bash
ps -ef
```
Lists all running processes.

```bash
kill <pid>
```
Terminates a process.

```bash
kill -9 <pid>
```
Forcefully terminates a process.

### Run a Process in Background

```bash
sleep 100 &
```

***

## User Accounts in Linux

### Why Create User Accounts?

Even though a **root user** exists, creating separate user accounts is important for:

- Security
- Accountability
- Application stability

### Types of Accounts

1. **Login Accounts** (for users)  
2. **Application Accounts** (for running services)

### Why Use App Accounts?

- Logs show which account executed the application  
- Files created by the app are owned by that account  
- If a human user account is removed, the app may fail  

**Best Practice:**
- Use dedicated application users

**Example:**
- For a payment app → create user `payment`  
- For a project → create user `roboshop`  

***

## User and Group Management

### Create a User

```bash
useradd mike
```

### Group Membership

- Each user has:
  - 1 primary group  
  - Up to 15 secondary groups  

**Example:**
- Mike belongs to `devops` group  
- If part of multiple teams → `devops`, `sre`

### Create a Group

```bash
groupadd devops
```

### Add User to a Group

```bash
usermod -a -G devops satyam
```

***

## File Ownership

### Change Ownership

```bash
chown owner:group fileName
```

**Example:**
```bash
chown ec2-user:devops devops.txt
```

***

## File Permissions

### Permission Format

```
rw-r--r--
```

- Owner | Group | Others

### Permission Values

- Read (r) = 4  
- Write (w) = 2  
- Execute (x) = 1  

### `chmod` Syntax

```bash
chmod <permissions> fileName
```

### Examples

1. Owner: full (rwx), Group: read + execute (rx), Others: execute (x)

```bash
chmod 751 fileName
```

2. Owner: full (rwx), Group: read (r), Others: execute (x)

```bash
chmod 741 fileName
```

3. **chmod 777**

- Grants full access to everyone  
- **Not recommended** due to security risks  

