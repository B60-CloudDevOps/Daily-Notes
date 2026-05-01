## 📌 1. Printing Specific Lines from a File (`sed`)

`sed` (Stream Editor) is used for filtering and transforming text.

### 🔹 Print lines from X to Y
```bash
sed -n -e '10,15p' /etc/passwd
🔹 Important Note
sed -n -e '10,15' /etc/passwd

❌ This will NOT print anything because -n suppresses output and no p (print) command is used.

🔹 More Examples
sed -n -e '10,13p' /etc/passwd    # Print lines 10 to 13
sed -n -e '10p' -e '15p' /etc/passwd  # Print lines 10 and 15
sed -n -e '10p' /etc/passwd       # Print only line 10
🔹 Show line numbers
cat -n /etc/passwd
✂️ 2. cut Command (Extract Columns)

Used to extract specific fields from a file.

🔹 Syntax
cut -d<delimiter> -f<fields> <file>
🔹 Examples
cut -d: -f1 /etc/passwd        # Extract first field (username)
cut -d: -f1,4 /etc/passwd      # Extract fields 1 and 4
🧠 3. awk Command (Text Processing)

Powerful tool for pattern scanning and processing.

🔹 Print last field of each line
awk -F: '{print $NF}' filename
-F: → sets delimiter as :
$NF → last field in each line
📝 4. Editing Files

Common editors:

vi / vim
nano
🔹 Example
vi filename
📂 5. Linux Directory Structure

Linux follows a hierarchical (tree-like) structure, NOT linear.

🔹 Root Directory
/
🔹 Important Directories
/home → user directories
/etc → configuration files
/var → logs and variable data
/usr → user programs
/bin → essential binaries
🌐 6. Downloading from Internet
🔹 Using curl
curl -O <url>
🔹 Using wget
wget <url>
curl → flexible (APIs, reading content)
wget → simple file downloads
📦 7. Package Management in Linux

In Linux, software installation is called package installation.

🔹 RPM (Red Hat Package Manager)
rpm -ivh package-name.rpm

⚠️ You must manually handle dependencies.

🔹 YUM / DNF (Recommended)
dnf install <package-name>
yum install <package-name>

✅ Automatically resolves dependencies.

🔹 Key Commands
List available packages
dnf list available
Count available packages
dnf list available | wc -l
List installed packages
dnf list installed
Count installed packages
dnf list installed | wc -l
🔄 8. System Updates
🔹 Update packages
dnf update
🔁 9. Check if Reboot is Required
dnf needs-restarting -r
🔹 Example Output

Core components that may require reboot:

glibc
kernel
linux-firmware
microcode_ctl
systemd

👉 If these are updated → Reboot required

🔃 10. System Restart & Shutdown
🔹 Restart system
init 6
🔹 Shutdown system
init 0
📊 11. Package Insight (Example)
dnf list available | wc -l   # ~32967 packages available
dnf list installed | wc -l   # ~546 packages installed

👉 Linux installs minimal packages by default; add as needed.

🚀 12. What’s Next?
👤 Creating user accounts
⚙️ Installing services
▶️ Starting & managing services
🧾 Summary
sed → line filtering
cut → column extraction
awk → advanced text processing
dnf/yum → package management
curl/wget → downloading files
Linux structure → hierarchical