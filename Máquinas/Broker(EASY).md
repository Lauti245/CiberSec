 https://www.youtube.com/watch?v=o6aRIbFuKNA
1. **Nmap scan:**
   - Several open ports were discovered.

2. **Port 80:**
   - Requires authorization.
   - Used default credentials (admin/admin) and gained access.
   - Page shows **ActiveMQ** but nothing of interest.

3. **ActiveMQ vulnerability search:**
   - Found the **ActiveMQ version** from the scan.
   - The version has a known **CVE for Remote Code Execution (RCE)**.

4. **Exploit the ActiveMQ service:**
   - Exploited the vulnerability and got a **reverse shell** on the system.

5. **Sudo permissions check:**
   - Running `sudo -l` revealed **NGINX** can be used with **root permissions**.

6. **NGINX configuration:**
   - `nginx -h` shows a parameter to set a custom **.conf** file.
   - Created a **.conf** file to enable **DAV service** for file uploads.
   - Set the **/root** directory as the initial directory.
   - Assigned a different port (since **port 80** was already in use).

7. **Start NGINX with the custom configuration:**
   - Ran `sudo nginx` with the custom **.conf**.
   - Checked running services with `ss -tlpn` and confirmed **port 1337** was active.

8. **File upload preparation:**
   - Since we can upload files to **/root**, we generated **SSH keys** using `ssh-keygen`.
   - Set the keys to be saved in **/root**.

9. **Upload SSH public key:**
   - Used `curl PUT` to upload the **public key** to **/root/.ssh/authorized_keys**.
   - Used `-d $(cat root.pub)` to send the content of the public key.

10. **SSH login as root:**
    - Successfully logged in using the private key: `ssh -i root root@localhost`.
    - Gained access to the system as **root**.