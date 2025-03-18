#suid_perm
- **Initial Reconnaissance with Nmap**
    
    - Identified open ports:
        - **Port 22**: SSH
        - **Port 80**: HTTP
- **Web Application Analysis**
    
    - Conducted **web fuzzing** on port 80 but found no significant results.
    - Discovered a web page that **analyzes Wireshark traces** provided by users.
- **Exploitation of Insecure Direct Object References (IDOR)**
    
    - Identified an **IDOR vulnerability**, allowing access to traces belonging to other users.
    - Obtained a trace containing **VSFTPD connection logs** with credentials transmitted in **plain text**.
- **Credential Reuse and Shell Access**
    
    - Used the extracted credentials to attempt authentication via **SSH**.
    - Successfully gained **shell access** to the system.
- **Privilege Escalation**
    
    - Identified **unusual permissions** on the system.
    - Found that **Python** had **SUID privileges**.
    - Leveraged Python's SUID to spawn a privileged Bash shell.
- **Root Access**
    
    - Successfully escalated privileges and obtained **root access**.