In this CTF we are provided with a domain name ```atlas.picoctf.net``` at port```60954```
Upon visiting the website we are greeted with the following landing page
![Landing_page.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/Trickster/Landing_page.png)

### Inspecting the URL and using BurpSuite is futile as there are no leaks in the source code of the website.

Here, the most obvious attack vector is to run a directory search on the website to find out additional directories. I use ```gobuster``` a tool that comes pre-installed with Kali Linux to look for the same
![gobuster.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/Trickster/gobuster.png)

We get a ```/uploads``` directory with a status code ```301``` which meant the server was redirecting us to a different webpage. Upon force-browsing the webpage we recieve a ```403 Forbidden Error```

Due to the time limitation of 30 mins of server runtime, my machine was not able to complete the directory search. 

I ran into a deadend here and looked up this CTF to see if there were other directories that are discovered during the search and turns out there is a directory ```/robots.txt```  with a status code of ```200 OK```meaning it is working completely fine and accessible to us. Navigating there gives us this page.
![robots-txt_page.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/Trickster/robots-txt_page.png)
Using BurpSuite or Inspecting doesn't yield any results.

This reveals to us another directory ```/instructions.txt```. Navigating there we get the following page
![instruction-txt_page.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/Trickster/instruction-txt_page.png)
Similarly, here the text is the only useful information we get from the webpage.

What seems to be the case here is that we are supposed to upload a file disguised as a ```.png```  file which will then give us some sort of access of the server. 

I could find anything related to this online so looked up the CTF again and saw that the thing I was looking for was a web shell which can generate a command-line interface to execute commands on the server remotely. [This is the tool that I used](https://gist.github.com/joswr1ght/22f40787de19d80d110b37fb79ac3985). 

Now, we know that the website is going to check for 
- either the hexadecimal PNG ```50 4E 47``` 
- or the word ```PNG``` itself

We will append this to the top of the file and then upload it into the website. 
- Converting the ```.php``` file into a ```.png``` file wont work as we would not be able to execute the shell remotely later.
- Therefore we have to rename the file to ```file.png.php``` with ```file.png``` being the filename. Also now we to drag and drop the folder in the upload box as it is not going to appear on the file explorer due to it still being a ```php``` file

We find that appending ```50 4E 47``` still leads to the file being detected as a non-png file, hence we will append ```PNG```

![php_payload_accepted.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/Trickster/php_payload_accepted.png)

Now, our payload has been successfully sent. Now we activate the payload by accessing the page where it is stored. The best guess we can make is ```/uploads/<file-name-of-payload>``` as we had seen earlier about the existence of ```/uploads``` directory.

![payload_executed.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/Trickster/payload_executed.png)

Now we can type  ```whoami``` and see the username and user basic commands but we seem to be to unable to traverse through directories

![using_the_webshell.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/Trickster/using_the_webshell.png)

So we use the find command to see if there is anything we can find and there is a LOT. Most of them are unaccessible, but not all of them.

![accessible_files_found.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/Trickster/accessible_files_found.png)

Sifting through each of them we quickly realise that the ```/usr``` files are unavailable for us, so that leaves with the three files towards the bottom ```instructions.txt```, ```robots.txt``` and ```GQ4DOOBVMMYGK.txt```. Visiting the third file, we finally see our flag.
![flag_found.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/Trickster/flag_found.png)
* * *
The flag is ```picoCTF{c3rt!fi3d_Xp3rt_tr1ckst3r_48785c0e}```


Certified expert trickster fr
