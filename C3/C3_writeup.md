## Provided with two files
- convert.py
- ciphertext

##  Hint
"Modern crypto schemes don't depend on the encoder to be secret, but this one does."
* * *
## 1. ```ciphertext``` (text file)
```
DLSeGAGDgBNJDQJDCFSFnRBIDjgHoDFCFtHDgJpiHtGDmMAQFnRBJKkBAsTMrsPSDDnEFCFtIbEDtDCIbFCFtHTJDKerFldbFObFCFtLBFkBAAAPFnRBJGEkerFlcPgKkImHnIlATJDKbTbFOkdNnsgbnJRMFnRBNAFkBAAAbrcbTKAkOgFpOgFpOpkBAAAAAAAiClFGIPFnRBaKliCgClFGtIBAAAAAAAOgGEkImHnIl
```
## 2. ```convert.py``` (python file)
```
import sys
chars = ""
from fileinput import input
for line in input():
  chars += line

lookup1 = "\n \"#()*+/1:=[]abcdefghijklmnopqrstuvwxyz"
lookup2 = "ABCDEFGHIJKLMNOPQRSTabcdefghijklmnopqrst"

out = ""

prev = 0
for char in chars:
  cur = lookup1.index(char)
  out += lookup2[(cur - prev) % 40]
  prev = cur

sys.stdout.write(out)
```

## What ```convert.py``` does
It takes multiple lines as input and peforms a cipher on each of the characters.
### Notes
- The input logic is probably faulty as it never stops taking input

![OG_convert.py_output.png](C3/OG_convert.py_output.png)
This can be fixed quite easily
- The lookups are setup incorrectly.
- Variable ```cur```  is an integer corresponding to every character possible in ```ciphertext```
- The output ```out``` of the file is a string of characters with each character of it correseponding to its equialent index in the ```ciphertext```

## Attempting to run the program through the contents of ```ciphertext```
- I tried running the code as is and as exepected the code was broken 
	![disfigured_converter_output.png](C3/disfigured_converter_output.png)
- I looked up on the internet to see if i could find something on this. I found a Medium Page where someone had solved an earlier version of the problem with the correct converter provided.
https://medium.com/@amosakogbe/picoctf-2024-write-up-a87028436556
- It turns out that the encoded string is actually a python code
	```
	#asciiorder
	#fortychars
	#selfinput
	#pythontwo
	
	chars = ""
	from fileinput import input
	for line in input():
	    chars += line
	b = 1 / 1
	
	for i in range(len(chars)):
	    if i == b * b * b:
	        print chars[i] #prints
	        b += 1 / 1
	
	```
- The code has comments hinting at the ASCII table.
	- ```#asciiorder \n fortychars``` is what I thought was the 40th character in the ASCII table which is ```(```. That's not very relevant.
	- We need some sort of string that we need to input into this program to get to the next step.
	- I tried:-
		-  The original ```ciphertext``` which gave me the result ```picoCTF{LgHDPt}```
		-  ```pythontwo``` judging from the comments written on the file which gave me the result ```picoCTF{yo}```

### This was the furthest I could go before running into a brick wall
