
#docker 
1. **Nmap scan:**
   - Identified open ports: **80** and **22**.

2. **Port 80:**
   - Found a blog site with a **login page** running on **Metabase**.

3. **Exploit discovery:**
   - Found an **unauthenticated Remote Code Execution (RCE)** exploit for Metabase.
   - Successfully used the exploit to obtain a **reverse shell**.

4. **Reverse shell limitations:**
   - The shell was **not a fully interactive tty**, making it difficult to work with.

5. **Docker container suspicion:**
   - The hostname appeared similar to a **serial number**, suggesting the environment might be a **Docker container**.

6. **Environment inspection:**
   - Using **printenv**, found **credentials** in **.dockerenv** for **SSH** access.

7. **SSH login:**
   - Logged in using the credentials found in the Docker environment.

8. **Kernel vulnerability:**
   - Ran **uname -r** and identified the kernel was vulnerable to a **local privilege escalation** (CVE-2023-2640).

9. **Exploitation:**
   - Used the vulnerability to **exploit the kernel** and gained **root shell** access.