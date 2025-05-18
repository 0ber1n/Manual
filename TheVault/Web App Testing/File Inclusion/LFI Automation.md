
### ffuf

You can fuzz with ffuf to find LFI, utilizing a wordlist for LFI

```CLI
ffuf -w LFI-Jhaddix.txt -u 'http://<IP>:<PORT>/index.php?language=FUZZ' -fs 2287
```
