In this CTF we are provided with a domain name ```saturn.picoctf.net:54260```
Upon visiting the website we are greeted with a simple login page
![Login_page.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/LocalAuthority/Login_page.png)

Trying to login in with random credentials gives us a failed login screen
![login_falied.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/LocalAuthority/login_falied.png)

Analysing the URL doesn't help much
![inspect_URL.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/LocalAuthority/inspect_URL.png)

We get a css file ```style.css``` but that isn't helpful either
![css_output.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/LocalAuthority/css_output.png)

Using BurpSuite to analyze the URL we see an interesting file ```secure.js```
![Information_disclosure_secure_js.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/LocalAuthority/Information_disclosure_secure_js.png)

Navigating to it we directly get the credentials for the login page
![secure_js_output.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/LocalAuthority/secure_js_output.png)

* * *
The flag is
```picoCTF{j5_15_7r4n5p4r3n7_05df90c8}```

