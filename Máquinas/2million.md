#json #command_injection #mysql #
### Exploitation and Vulnerability Analysis Process

1. **Initial Scan with Nmap**
    
    - Identified **port 80** as open.
2. **Web Exploration**
    
    - Edited the `/etc/hosts` file to access the web application.
    - Found a JavaScript file located at `/invite`.
3. **Analyzing the JavaScript File**
    
    - Used a beautifier to format and understand the JavaScript code.
    - Discovered an encrypted message in the responses.
4. **Decrypting the Message with CyberChef**
    
    - Used **CyberChef** to decrypt the message.
    - Encountered an HTTP **301 Moved Permanently** status, indicating a wrong path.
    - Eventually retrieved the invitation code.
5. **Registration and Authentication Process**
    
    - Decoded the invitation code using:
        `echo "NUU5U1ctNzVCWTktTDhTMUItWklIREo=" | base64 -d`  
        
    - Used the code to register and log in.
6. **Vulnerability Research**
    
    - Looked for vulnerabilities on the web application.
    - Intercepted requests using **Burp Suite**.
    - Tested shorter paths and found one revealing allowed actions.
7. **Admin Endpoint Analysis**
    
    - Explored admin endpoints and selected the one to update user settings.
    - Fixed issues with the `Content-Type` by setting it to `application/json`.
    - Added missing parameters (`{}`).
    - Successfully escalated privileges to admin.
8. **Shell Injection via VPN Generation Option**
    
    - Discovered a code injection vulnerability in the VPN generation feature.
    - Gained a shell on the server.
9. **Information Gathering**
    
    - Found a `.env` file containing database credentials.
    - Accessed the MySQL database using the credentials.
    - Located a hashed password but couldn’t crack it.
    - Checked `/etc/passwd` for users and found the `admin` user.
    - Tried the same password, and it worked.
    - Retrieved the `user.txt` file.
10. **Privilege Escalation**
    
    - Searched for files owned by the `admin` user:
        `find / -user admin 2>/dev/null | grep -v '^/sys\|^/proc\|^/run'`
        
    - Found an email-related file.
    - Investigated relevant CVEs.
    - Found a proof-of-concept on GitHub.
11. **Exploitation Using the CVE**
    
    - Compressed and downloaded the proof-of-concept code from the machine.
    - Followed the steps and executed the exploit.
    - Gained root access.