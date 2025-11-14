
### To bypass rate limit:
1) Add these headers to the request and send in repeater until locked out:
	```
	X-Real-IP: 1.2.3.4
	X-Forwarded-For: 1.2.3.4
	X-Originating-IP: 1.2.3.4
	Client-IP: 1.2.3.4
	True-Client-IP: 1.2.3.4
	```
2) When locked out, increment by 1. Then start deleting headers until you get the blocked error.
3) Once found, thats the header to increment in pitch fork attack to bypass.
4) When the right header is found, if nothing comes back, we are looking at timing then. So make password suuuuuuper long.
5) run the pitchfork attack and longest out of norm response wins. Make sure to add the response heading in the intruder results.