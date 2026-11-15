# Activity 15.4 — Investigating File Upload Attacks

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 03  
> **Course Lesson:** 15  
> **Environment:** DVWA — forenseLinux and forenseWin VMs  
> **Status:** Completed

## 1. Objective

Investigate an unrestricted file upload vulnerability in DVWA and identify the server-side artifacts associated with the uploaded files.

The exercise demonstrates how a web application that does not properly validate uploaded files may allow an attacker to place executable content within a web-accessible directory.

The laboratory then examines the resulting connection evidence and the uploaded file directory on the Linux server.

The investigation focuses on:

- Testing whether the application accepts a PHP file.
- Identifying the upload destination.
- Understanding the reverse-shell behavior demonstrated in the isolated lab.
- Observing the connection recorded by Ncat.
- Identifying uploaded files in the server directory.
- Correlating the findings with Apache access logs.

## 2. Environment

| Item | Details |
|---|---|
| Application | DVWA |
| Web Server | `forenseLinux` |
| Server IP | `192.168.98.10` |
| Attacker Workstation | `forenseWin` |
| Attacker IP | `192.168.98.30` |
| Application Module | File Upload |
| Security Level | Low |
| Upload Directory | `/var/www/html/dvwa/hackable/uploads/` |
| Test File | `teste.php` |
| PHP Artifact | `php_reverse_shell.php` |
| Connection Utility | Ncat |
| Listening Port | `4444` |
| Web Server Log | `/var/log/apache2/access.log` |

The exercise was performed in the controlled DVWA laboratory.

The course temporarily adjusted Windows network and real-time protection settings to allow the isolated demonstration. Such changes should never be applied to a production or personal workstation.

## 3. Technical Concepts

### Unrestricted File Upload

A file upload vulnerability occurs when an application accepts files without sufficient validation or safe handling.

Inadequate controls may allow an attacker to upload content that the server interprets or executes.

A PHP file uploaded into a web-accessible directory may be particularly dangerous when the web server is configured to execute PHP in that directory.

### Webroot and Executable Uploads

The webroot is the directory from which the web server serves application content.

When an uploaded file is stored in an executable location, an attacker may be able to request that file through a browser.

If the server processes the file as executable code, the consequences can include server-side code execution.

### Reverse Shell

A reverse shell is a communication pattern in which a process on the target system initiates an outbound connection to a listener controlled by another system.

In this activity:

| Component | Value |
|---|---|
| Target Web Server | `192.168.98.10` |
| Attacker Workstation | `192.168.98.30` |
| Attacker Listening Port | `4444` |
| Connection Tool | Ncat |
| Target Process Context | `www-data` |

The exercise demonstrates why allowing executable file uploads is dangerous.

The PHP reverse-shell source code is not reproduced in this public README.

### Ncat

Ncat is a network utility included in the Nmap project.

It can listen for incoming TCP connections and display data received through the connection.

In the laboratory, Ncat was used to observe the incoming connection from the web server.

### Apache Upload Directory

The DVWA application stores uploaded files in:

```text
/var/www/html/dvwa/hackable/uploads/
```

Examining this directory provides evidence of files placed on the server through the application.

The filename, file size, timestamp, and ownership can help distinguish normal uploads from suspicious content.

## 4. Procedure

### Step 1 — Open the File Upload Module

The DVWA application was accessed from the Windows workstation:

```text
http://192.168.98.10/dvwa
```

The **File Upload** module was selected.

The page displayed a form that allowed the user to select a local file and upload it to the application.

### Step 2 — Create a Basic PHP Test File

The course used Notepad to create a simple file containing:

```text
teste
```

The file was saved as:

```text
teste.php
```

The Save as type option was set to **All Files** so that Windows would preserve the `.php` extension.

This test was intended to verify whether the application accepted a PHP file.

### Step 3 — Upload the Test File

The file:

```text
teste.php
```

was selected in the DVWA upload form and submitted.

The application accepted the upload and displayed the path where the file had been saved.

The course identified the web-accessible upload directory:

```text
http://192.168.98.10/dvwa/hackable/uploads/
```

This demonstrated that the application accepted a file with a server-side executable extension.

### Step 4 — Prepare the Controlled Reverse-Shell Demonstration

The course then used a PHP reverse-shell artifact configured to connect from the web server to the attacker workstation.

The relevant connection parameters were:

| Parameter | Value |
|---|---|
| Callback Address | `192.168.98.30` |
| Callback Port | `4444` |
| Target Server | `192.168.98.10` |
| Target Account | `www-data` |

The PHP file was named:

```text
php_reverse_shell.php
```

The supplied artifact used PHP socket and process functionality to establish a callback connection and associate it with an interactive shell.

The executable reverse-shell source code is intentionally omitted from this public documentation.

### Step 5 — Upload the PHP Artifact

The file:

```text
php_reverse_shell.php
```

was uploaded through the DVWA File Upload module.

The vulnerability allowed the file to be placed in the application upload directory.

The server-side directory was later examined to validate the presence of the uploaded artifact.

### Step 6 — Observe the Connection with Ncat

On the Windows attacker workstation, the course opened a terminal and started Ncat in listening mode:

```cmd
ncat -nlvp 4444
```

The supplied output was:

```text
Ncat: Version 7.92 ( https://nmap.org/ncat )
Ncat: Listening on :::4444
Ncat: Listening on 0.0.0.0:4444
Ncat: Connection from 192.168.98.10.
Ncat: Connection from 192.168.98.10:38624.
SOCKET: Shell has connected! PID: 28723
```

The connection originated from:

```text
192.168.98.10
```

The source port recorded by Ncat was:

```text
38624
```

The target process context was then examined.

The following command was entered in the connected shell:

```bash
id
```

The output was:

```text
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

This identified the account under which the web server process was running.

The hostname was examined:

```bash
hostname
```

The output was:

```text
ip-192-168-98-10
```

The network interfaces were examined:

```bash
ip a
```

The recorded output included:

```text
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever

2: ens5: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc mq state UP group default qlen 1000
    link/ether 12:30:6c:50:64:d5 brd ff:ff:ff:ff:ff:ff
    altname enp0s5
    inet 192.168.98.10/24 metric 100 brd 192.168.98.255 scope global dynamic ens5
       valid_lft 2142sec preferred_lft 2142sec
    inet6 fe80::1030:6cff:fe50:64d5/64 scope link
       valid_lft forever preferred_lft forever
```

The output demonstrated that the connection reached the server and that the resulting shell operated under the `www-data` account.

### Step 7 — Investigate the Server Upload Directory

The investigation returned to the Linux server.

The Apache log was identified as a source of information about requests to the upload functionality.

Because the upload itself does not necessarily place the file content in a URL parameter, the access log may record the request without revealing the uploaded PHP source.

The investigation therefore examined the upload directory directly.

The following commands were executed:

```bash
cd /var/www/html/dvwa/hackable/uploads/
```

```bash
ls -la
```

The supplied output was:

```text
total 20

drwxrwxrwx 2 root     root     4096 Jul 10 14:06 .
drwxrwxrwx 5 root     root     4096 Jul  9 13:12 ..
-rwxrwxrwx 1 root     root      667 Jul  9 12:55 dvwa_email.png
-rw-r--r-- 1 www-data www-data 3507 Jul 10 14:06 php_reverse_shell.php
-rw-r--r-- 1 www-data www-data    5 Jul 10 14:19 teste.php
```

The directory contained three files:

| File | Size | Owner | Recorded Timestamp |
|---|---:|---|---|
| `dvwa_email.png` | 667 bytes | `root` | Jul 9, 12:55 |
| `php_reverse_shell.php` | 3507 bytes | `www-data` | Jul 10, 14:06 |
| `teste.php` | 5 bytes | `www-data` | Jul 10, 14:19 |

The file `php_reverse_shell.php` was identified as the suspicious artifact.

Its contents could be examined during forensic analysis to identify the callback address and port used by the laboratory demonstration.

## 5. Expected Results

The activity demonstrates a file upload vulnerability that allowed PHP files to be stored in the application upload directory.

The resulting connection and filesystem evidence include:

| Evidence | Result |
|---|---|
| Uploaded Test File | `teste.php` |
| Uploaded PHP Artifact | `php_reverse_shell.php` |
| Upload Directory | `/var/www/html/dvwa/hackable/uploads/` |
| Ncat Listener Port | `4444` |
| Connecting Host | `192.168.98.10` |
| Attacker Workstation | `192.168.98.30` |
| Connection Source Port | `38624` |
| Shell Process Context | `www-data` |
| UID | `33` |
| GID | `33` |
| Hostname | `ip-192-168-98-10` |

The results demonstrate the impact of allowing executable files to be uploaded into a web-accessible directory.

## 6. Technical Analysis

### Upload Validation Failure

The application accepted a PHP file through a feature intended for uploading content.

The test file demonstrated that the application did not sufficiently restrict the submitted extension.

The later uploaded PHP artifact demonstrated the impact when the web server was configured to execute uploaded PHP content.

### Reverse Connection Evidence

Ncat recorded an incoming connection from:

```text
192.168.98.10
```

to the listener on:

```text
192.168.98.30:4444
```

The connection record provides a network indicator that can be correlated with the uploaded file and the application's access logs.

### Execution Context

The output of:

```bash
id
```

identified the shell context as:

```text
uid=33(www-data) gid=33(www-data)
```

This is important because it identifies the privileges available to the process.

The evidence does not indicate that the session had root privileges.

The process ran under the web server account.

### Filesystem Evidence

The upload directory listing revealed the files created by the exercise.

The suspicious file was:

```text
php_reverse_shell.php
```

Its ownership was:

```text
www-data www-data
```

Its recorded size was:

```text
3507 bytes
```

The file's name, extension, ownership, location, and content are all relevant to the investigation.

### Correlation of Evidence

A complete investigation should correlate:

1. Apache access records for the upload endpoint.
2. The uploaded PHP file.
3. File ownership and timestamps.
4. The Ncat connection record.
5. The process identity reported by `id`.
6. The server hostname and network configuration.

Together, these findings provide a coherent explanation of the file upload and subsequent server-side execution.

### Defensive Recommendations

OWASP recommends a layered approach to secure file uploads:

- Maintain an allowlist of permitted file extensions.
- Validate file content rather than trusting the submitted MIME type.
- Generate server-side filenames.
- Limit file size and filename length.
- Restrict upload access to authorized users.
- Store uploaded files outside the webroot whenever possible.
- Prevent uploaded files from being interpreted as executable code.
- Scan files for malicious content.
- Apply appropriate permissions to upload directories.
- Monitor unexpected file creation and execution.

A web-accessible upload directory should not execute user-supplied server-side scripts.

## 7. Results and Interpretation

The activity demonstrated the consequences of an unrestricted file upload vulnerability.

The application accepted a PHP file and stored it in a web-accessible directory.

The laboratory then recorded a connection from the server to the Ncat listener on the attacker workstation.

The shell operated under the `www-data` account, and the subsequent examination of the upload directory identified the uploaded PHP artifact.

The combination of network and filesystem evidence demonstrates how an investigator can reconstruct the sequence of a file upload attack.

## 8. Concepts Practiced

- File Upload vulnerability
- DVWA
- PHP upload handling
- Webroot
- Executable file uploads
- Reverse shell concept
- Ncat
- TCP listener
- Network connection analysis
- Process identity
- Linux users and groups
- `id`
- `hostname`
- `ip a`
- Apache access logs
- Upload directory examination
- File ownership
- File timestamps
- Filesystem evidence
- Incident reconstruction
- Secure upload validation

## 9. Evidence

**Required screenshot: Activity 15.4 — Step 6 — PDF page 4.**

The screenshot should display the Ncat listener and the incoming connection from:

```text
192.168.98.10
```

It should also show the connection to port:

```text
4444
```

The evidence should include the shell connection confirmation and, where visible, the output identifying the `www-data` account.

The exact screenshot described in the supplied evidence summary corresponds to this step.

[View Class Evidence PDF](../evidences.pdf)

## References

- [OWASP — File Upload Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html)
- [OWASP — Testing for Malicious File Upload](https://owasp.org/www-project-web-security-testing-guide/)
- [OWASP — Unrestricted File Upload](https://owasp.org/www-community/vulnerabilities/Unrestricted_File_Upload)
- [Nmap — Ncat Reference Guide](https://nmap.org/ncat/guide/)
- [Apache HTTP Server — Log Files](https://httpd.apache.org/docs/current/logs.html)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md) · [Next Activity — 15.5](../atividade-15.5-forca-bruta/README.md)
