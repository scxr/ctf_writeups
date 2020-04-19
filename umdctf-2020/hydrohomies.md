# UMD CTF 2020

##  Hydro Homies - Stegonography (300pts)
What can i say about this challenge? Well, it will definitely make you bang your head against the wall, thats for sure however i have to say, its probably one of my favourite ctf challenges ive ever done, very interesting and different to what im used to. Which was fun for sure, so lets get into it.
So i began by scanning through the wav to maybe audibly hear pitch changes or freq changes but heard nothing except an amazing review so i opened up the image and saw wonderful bernie:
[Imgur](https://imgur.com/tEHILZz.jpg "")
had a good laugh at the S tier meme then ran strings on it, starting with `strings -n 10` where i was greeted with :
![Imgur](https://imgur.com/Pv6MgjP.jpg)
I prayed to the holy gods that `st4yhydr8ted` gave me the easiest 300 points ever, however sadly not, so i opened up steghide on the wav file and tried using the password and it worked!
I got the output of  (imgur seems to be blocking my files now) :
```
> steghide extract -sf water_review.wav  
Enter passphrase:  
the file "secret_documents.zip" does already exist. overwrite ? (y/n) y  
wrote extracted data to "secret_documents.zip".
```
So then i unzipped it and was greeted with:

![Screenshot-from-2020-04-19-16-12-27.png](https://i.postimg.cc/2601Lqq2/Screenshot-from-2020-04-19-16-12-27.png)
The owner of babeline brook seemed like an interesting person so i reverse image searched and found it was a man called : "Jorge Luis Borges"
So i googled about him and found the [Library of babel]([https://libraryofbabel.info/](https://libraryofbabel.info/)) so i had a look around and what it was and it was very interesting. Noting the filenames i noticed that this was definitely the right place. For the library of babel you need the following: The hex (the place the book is), The shelf (the shelf the books is on), The wall (the wall the book is on), The volume (the volume of book) and The page, the page the flag should hopefully be on. This is easy enough to see from filenames that that info is :
Wall num: 3
Shelf num: 3
Volume num: 15
Page num : 135
However the hex is missing and this is what took me approximately 3 hours total time to figure out, as i had previously skipped an easy step. The hex can be found in the `babeling_book_h3xx3h` file by catting it. When you cat the file you can see:
![img](https://i.postimg.cc/L5LjWcmr/Screenshot-from-2020-04-19-16-23-26.png)
So i copied the text into a new file and started running all sorts on it, then i was messing about on the library of babel looking at different books and noted the url format. The url format is : `https://libraryofbabel.info/book.cgi?{hexnum}-w{wallnum}-s{shelfnum}-v{volnum}:{pagenum})`
So i put my stuff in there and got to the page: ![img](https://i.postimg.cc/xCcF71Jq/Screenshot-from-2020-04-19-16-27-23.png)
I stared wondering why on earth it didnt work, as i was searching for "UMD" however i then searched for "flag" where i finally saw : `the flag is hydrate or diedrate homies`
I cried a few tears of joy and drank my pepsi max in a victory fashion.
flag : UMDCTF-{hydrate or diedrate homies}
