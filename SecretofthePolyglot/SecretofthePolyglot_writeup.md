## Files provided
- ```flag2of2-final.pdf```
* * *
This is a relatively straight-forward challenge. It is mentioned that we need to open the file in fidderent formats in order to get all the parts of the flag
- One of the methods is obviously .pdf
- I tried UTF-8 but that didnt work
### Opening the file in (.pdf) format
This gives us the last part of the flag 
![pdf_output.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/SecretofthePolyglot/forensic_analysis/pdf_output.png)
### Opening the file in (.docx) format
![docx_output_pt1.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/SecretofthePolyglot/forensic_analysis/docx_output_pt1.png)
Resizing the tiny image present at the centre gives us the first part of the flag
![docx_output_pt2.png](https://github.com/rugbedbugg/MFC_picoCTF/blob/main/SecretofthePolyglot/forensic_analysis/docx_output_pt2.png)
* * *
I tried to combine both of them together into a single word which turned out to be the correct flag
```picoCTF{f1u3n7_1n_pn9_&_pdf_90974127}```
