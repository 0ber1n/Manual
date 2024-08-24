
Once in, stabalize the shell using python 

$ python3 -c 'import pty;pty.spawn("/bin/bash")' 

$ python3 -m http.server 8888 

Stabilize your shell: 

1. Import pty module and spawn bash shell: 
 $ python3 -c 'import pty;pty.spawn("/bin/bash")' 
    

3. Press CTRL + Z to background process and get back to your host machine 
    
4. Use stty command to set terminal line settings and foreground back the target terminal: COPY
$ stty raw -echo; fg 
    
5. Set the terminal emulator to xterm: COPY 
$ exportTERM=xterm  
    
6. Press Enter 
    

From <[https://brain2life.hashnode.dev/how-to-stabilize-a-simple-reverse-shell-to-a-fully-interactive-terminal](https://brain2life.hashnode.dev/how-to-stabilize-a-simple-reverse-shell-to-a-fully-interactive-terminal)>



to get stuff back, run a python server 

$ python3 -m http.server 9999 