In this CTF we are provided with a domain name ```saturn.picoctf.net:54260```
Upon visiting the website we are greeted with a simple login page
![Login_page.png](:/9a9ff66094744bd8b401ab8b72592a9a)

Trying to login in with random credentials gives us a failed login screen
![login_falied.png](:/1eb89c36665a4d768d0bef11126b96d4)

Analysing the URL doesn't help much
![inspect_URL.png](:/646d3a445a7f402e82c421a121a37311)

We get a css file ```style.css``` but that isn't helpful either
![css_output.png](:/2c441778c60a4970b5fdc0585a079b1b)

Using BurpSuite to analyze the URL we see an interesting file ```secure.js```
![Information_disclosure_secure_js.png](:/4ad028bbd03b4897b35674938d389798)

Navigating to it we directly get the credentials for the login page
![secure_js_output.png](:/189515a5f523476cb8d48f69acba15b3)

* * *
The flag is
```picoCTF{j5_15_7r4n5p4r3n7_05df90c8}```

