Server message block

Parecido a ftp , puede que deje entrar con anonymous o guest account

comando para entrar smbclient \\\\{IP}\\{share}

[-L|--list=HOST] : Selecting the targeted host for the connection request.
Running the command above, we see that four separate shares are displayed. Let us go through each of
them and see what they mean.
- ADMIN$ - Administrative shares are hidden network shares created by the Windows NT family of operating systems that allow system administrators to have remote access to every disk volume on a network-connected system. These shares may not be permanently deleted but may be disabled.
- C$ - Administrative share for the C:\ disk volume. This is where the operating system is hosted.
- IPC$ - The inter-process communication share. Used for inter-process communication via named pipes and is not part of the file system.
- WorkShares - Custom share.
