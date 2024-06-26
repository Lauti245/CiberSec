 - script  /dev/null -c bash
 -  ctrl z para suspender el proceso
 - stty raw -echo;fg
 - reset xterm
 - export TERM= XTERM
-------------------
python3 -c 'import pty:pty.spawn("/bin/bash")'
ctrl z 
export TERM=XTERM

