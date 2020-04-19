# UMD CTF 2020

## Fragile Foundations - Crypto (300pts)
To start this challenge i catted the file, where i was overwhelmed with text, however i did notice that it ended with '==' which is usually an indicator of base64, base64 string lengths are a multiple of 4 so i fired up a quick python interpreter and did the following:
```python
>>> mystring = open('ciphertext','r').read()  
>>> length = len(mystring)  
>>> print(length / 4)  
1710430.0
```
The .0 indicates it is indeed a multiple of 4 so what i then did was headed over to my goto [b64 decoder]([https://www.base64decode.org/](https://www.base64decode.org/)) and stuck the text in as a file and it returned me something, which i ran the above script on and realised it was again a b64 string. So then i realised that due to the length of this im going to have to script this. So i fired up nvim and got to work.
```python
import base64 
num = 1
while 1:
    if num == 1:
        with open('ciphertext','r') as f:
            txt = f.read()
            f.close()
    else:
        filepath = 'decodenum{}'.format(num-1)
        with open(filepath, 'r') as f:
            txt = f.read()
            f.close()
    msg_bytes = base64.b64decode(txt)
    msg = msg_bytes.decode('ascii')
    filepath = 'decodenum{}'.format(num)
    with open(filepath, 'w') as o:
        o.write(msg)
        o.close()
    num +=1
    print('Another one : decodenum{}'.format(num))
```
As you can probably tell by the `while 1` im a *lazy* coder, you could use a try except to catch it when it gets to the end, however i just let it error out which stops the program just fine ;). So i will explain this code however its relatively simple. 
```python
num = 1  
while 1:  
	if num == 1:  
		with open('ciphertext','r') as f:  
		txt = f.read()  
		f.close()  
	else:  
		filepath = 'decodenum{}'.format(num-1)  
		with open(filepath, 'r') as f:  
		txt = f.read()  
		f.close()
```
So, what this does is allows us to read the file that was decoded last, we do the `if num==1` as my original was called ciphertext and i didnt want to `:wq` and change it, again *lazy* ;). We need the `num-1` as the num increments at the end of the while loop, so once decodenum2 has been written the number would now be 3 but we need to read from the previous one. 

```python
    msg_bytes = base64.b64decode(txt)
    msg = msg_bytes.decode('ascii')
    filepath = 'decodenum{}'.format(num)
    with open(filepath, 'w') as o:
        o.write(msg)
        o.close()
    num +=1
    print('Another one : {}'.format(filepath))
```
We start by decoding the base64 string and then decoding that to ascii value to make it easy for the open to read it. We write our text, close it and then print where we wrote it.  The `b64decode` will throw the error and tell us when we have done.
So lets run it !
![Imgur](https://imgur.com/49rdiQ2.jpg "imafe")

And there we go, now we cat decodenum42 and get the flag to be:
UMDCTF-{b@se64_15_my_f@v0r1t3_b@s3} 
