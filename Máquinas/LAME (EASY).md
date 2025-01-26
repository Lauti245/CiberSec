### Security Assessment Workflow

1. **Initial Reconnaissance with Nmap**
    
    - Scanned and identified open ports:
        - Port 21: FTP
        - Port 22: SSH
        - Port 139: Samba (VSFTP)
2. **Attempted Exploitation of VSFTP**
    
    - Discovered a known vulnerability in VSFTP.
    - Attempted to exploit it, but the attempt was **unsuccessful**.
3. **Exploration of Samba Service (Port 22)**
    
    - Investigated Samba version 3.2.20 for vulnerabilities.
    - Identified a compatible **exploit** for the version in use.
4. **Exploitation of Samba Vulnerability**
    
    - Successfully exploited the vulnerability and gained **root access** to the system.
5. **Post-Exploitation Activities**
    
    - Navigated through the file system.
    - Retrieved **flags** as part of the assessment.