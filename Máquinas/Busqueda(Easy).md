#partial_route
- **Initial Reconnaissance with Nmap**
    
    - Identified open ports:
        - **Port 22**: SSH
        - **Port 80**: HTTP
- **Web Application Analysis**
    
    - Discovered a web service running on **port 80**, utilizing a Python library called **Searchor**.
    - Identified that the application was using an **outdated version** of the library, which is vulnerable to **Remote Code Execution (RCE)**.
- **Exploitation of RCE Vulnerability**
    
    - The exploit leveraged the **unsanitized use of `eval`**, allowing arbitrary command execution.
    - Successfully obtained a **reverse shell**.
- **Post-Exploitation and Credential Discovery**
    
    - Conducted a file enumeration and discovered credentials inside a **.git/config** file.
    - The credentials also revealed a **new domain**.
- **Accessing Gitea and Privilege Escalation**
    
    - Accessed the discovered domain, which hosted a **Gitea** instance.
    - Logged in using the retrieved credentials but found no significant information.
    - Identified **a Python-based binary** that we were allowed to execute, functioning as a limited Docker wrapper.
    - Executed `docker ps` and `docker inspect`, revealing **administrator credentials for Gitea**.
- **Source Code Analysis and Exploitation**
    
    - With administrator access to Gitea, obtained the **source code** of the script that we had execution rights on.
    - Identified that the script **calls another file using a relative path**, meaning it searches for the file in the **execution directory**.
    - Created a **malicious file** with the same name in the `/tmp` directory, embedding a command to obtain a shell.
- **Gaining Root Access**
    
    - Executed the modified binary from `/tmp`, successfully gaining a **root shell**.