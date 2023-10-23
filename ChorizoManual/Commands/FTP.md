|   |   |   |
|---|---|---|
|?|_to request help or information about the FTP commands_|   |
|ascii|_to set the mode of file transfer to ASCII  <br>(this is the default and transmits seven bits per character)_|   |
|binary|_to set the mode of file transfer to binary  <br>(the binary mode transmits all eight bits per byte and thus provides less chance of a transmission error and must be used to transmit files other than ASCII files)_|   |
|bye|_to exit the FTP environment (same as quit)_|   |
|cd|_to change directory on the remote machine_|   |
|close|_to terminate a connection with another computer_|   |
||close brubeck|closes the current FTP connection with brubeck,  <br>  but still leaves you within the FTP environment.|
|delete|_to delete (remove) a file in the current remote directory (same as rm in UNIX)_|   |
|get|_to copy one file from the remote machine to the local machine_|   |
||get ABC DEF|copies file ABC in the current remote directory to (or on top of) a file named DEF in your current local directory.|
||get ABC|copies file ABC in the current remote directory to (or on top of) a file with the same name, ABC, in your current local directory.|
|help|_to request a list of all available FTP commands_|   |
|lcd|_to change directory on your local machine (same as UNIX cd)_|   |
|ls|_to list the names of the files in the current remote directory_|   |
|mkdir|_to make a new directory within the current remote directory_|   |
|mget|_to copy multiple files from the remote machine to the local machine;  <br>  you are prompted for a y/n answer before transferring each file_|   |
||mget *|copies all the files in the current remote directory to your current local directory, using the same filenames. Notice the use of the wild card character, *.|
|mput|_to copy multiple files from the local machine to the remote machine;  <br>  you are prompted for a y/n answer before transferring each file_|   |
|open|_to open a connection with another computer_|   |
||open brubeck|opens a new FTP connection with brubeck;  <br>  you must enter a username and password for a brubeck account  <br>      (unless it is to be an anonymous connection).|
|put|_to copy one file from the local machine to the remote machine_|   |
|pwd|_to find out the pathname of the current directory on the remote machine_|   |
|quit|_to exit the FTP environment (same as bye)_|   |
|rmdir|_to to remove (delete) a directory in the current remote directory_|   |