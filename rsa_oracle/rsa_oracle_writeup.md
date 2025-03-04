## Files provided
- ```password.enc``` (plaintext file)
- ```secret.enc``` (unknown file type)
## Additional information provided
- Domain name ```titan.picoctf.net``` at port ```53472```
* * *
## Attempt to access domain
- Using ```nmap``` on the domain that ```53472``` is indeed the only open port on the server

	![nmap_output.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/rsa_oracle/nmap_output.png)
- The service wont let me decrypt the password so I ask it to encrypt it instead to see if I can get some information. Sure enough, it does give us valuable information.
	- ## Information Discloure
		The encryption method first converts the cleartext to ```Hex``` and then applies ```m ^ e mod n (aka RSA encyrption)```  and finally outputs the resultant string.
## RSA attack on ```password.enc```
The obvious attack vector at this point is to decrypt the RSA encoded file. I use this script I found on the internet to decrypt the encoded file. The script uses the ```pwn``` library in Python which contains a huge set of tools for ethical hacking purposes. The script also converts the Hex value back into plaintext.
```
from pwn import *
		
context.log_level='critical'
p = remote("titan.picoctf.net", 61923)

p.recvuntil(b"decrypt.")

with open("password.enc") as file:
    c = int(file.read())

p.sendline(b"E")
p.recvuntil(b"keysize): ")
p.sendline(b"\x02")
p.recvuntil(b"mod n) ")

c_a = int(p.recvline())

p.sendline(b"D")
p.recvuntil(b"decrypt: ")
p.sendline(str(c_a*c).encode())
p.recvuntil(b"mod n): ")

password = int(p.recvline(), 16) // 2
password = password.to_bytes(len(str(password))-7, "big").decode("utf-8")

print("Password:", password)
```

### We cleanly get the password
![cleartext_password.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/rsa_oracle/cleartext_password.png)
Now as given in the hints, we simply run the command
```openssl enc -aes-256-cbc -d -in secret.enc``` to decrypt the flag
* * *
We are propmpted to enter the password after which we receive our flag
```picoCTF{su((3ss_(r@ck1ng_r3@_24bcbc66}```
