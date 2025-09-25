# HackornCTF 2025 Writeup

## sanity check
### Description
The Hackorn's ticketing system is compromised as the organizers announced.

Update: announcement tab is hiding some secret, reveal to see through. #PlainSight

### Solution

Within the Hackor[n] discord server under the announcements channel, there is a hidden flag within the first message sent, which can be revealed by clicking on it.

## the easy flag
### Description
Slippery snakes swiftly slide, seekers seek sly secrets stashed, flag flickers fast.. find it first!

Link to file : easychallenge.py

Ref: SPL{some_random_text}

### Solution

Running the given Python file prints a message to the terminal, this message once wrapped in SPL{} gives the flag.

## EncTy
### Description
51 4E 4A 7B 7A 39 32 39 39 64 31 79 30 31 38 35 32 39 36 31 61 7A 79 63 31 31 39 79 30 35 32 63 39 36 79 79 37 35 33 32 38 32 63 31 36 63 31 64 35 79 37 39 61 34 30 35 31 7A 63 30 32 32 30 39 38 38 38 33 7D

### Solution
The description consists of a message in hexidecimal (identifiable by pairs of numbers and letters) once decoded returns an encoded flag. Since we know the flag starts with SPL we can find the Unicode difference, from this difference we can find the offset. Using a ceasar cipher python script we can easily shift the flag values by the offset.
```
def decrypt(text, key):
    result = ""

    for char in text:
        if char.isalpha():
            upper = char.isupper()
            num = ((ord(char.upper()) - 65) + (26 - key)) % 26
            new_char = chr(num + 65)

            if not upper:
                new_char = new_char.lower()

            result += new_char

        else:
            result += char

    return result
```

## copy paste
### Description
Attackers often test or leak credentials on public paste sites. Can you find the leaked credential?

Link: copy_paste.zip

Sample: SPL{some_random_text}

### Solution
This challenge provides us with a server log represented in a 1510 line txt file. The file is stored completely in plain text, making it easy to search for the username and password for a now compromised account. Once the password has been found the flag can be created by using the format SPL{username_password}.

## SwArmy
### Description
Decode it, that simple :

Sigurd Petter Ludvig { Sexa Trea Nolla Caesar Tvåa Filip Ett Caesar Nolla Erik Erik Ett Bertil Åtta David Sju David Adam Femma Sju Caesar Filip Åtta Nia Trea Sexa Adam Erik Sju Erik Sju Åtta Tvåa Sju Fyra Adam Bertil Adam Nolla Bertil Filip David Sju Sexa Femma Filip Erik Ett Nolla Adam Tvåa Nolla David Filip Erik Femma Åtta Nolla Filip Nia Erik Erik Caesar Caesar }

### Solution
Seeing that ```Sigurd Petter Ludvig``` is the start of the text, it can be presumed that we will have to take the first letter of each word. Doing so returns SPL{} correctly but includes the character Å due to the word Åtta. After researching the term Åtta, we can find that it is Swedish for the number 8. The numbers for 0 - 10 in Swedish are ```noll, ett, två, tre, fyra, fem, sex, sju, åtta, nio, tio```. Using this information, you can replace each Swedish word for its corrisponding letter, with the rest of the non-Swedish words just concatonating their first letter. A simple Python script can help automate this task.

```
message = "S P L { test message }"

for i in message.split(" "):
    print(i[0], end='')
```

## mal medium
### Description
Can you trace the infection path and identify the C2 domain?

Source: mal_medium.zip

### Solution
Opening the zip file provided we get 4 files: network.log, pastebin.txt, strings.txt, and vt_reports.json. Within pastebin.txt there are various strings of seeming random numbers and letters. However, paste 9 is much shorter than the rest; inspecting it further we can surmize it is base64. Placing this string of text in a txt file allows us to run ```base64 -d file.txt``` which echos into the terminal flag{domain}. This allows us to easily find the C2 domain and submit the flag.

## dns sluth
### Description
A suspicious phishing email claimed to come from support-hackorn.secpen.org - as reported. Goal: Identify the suspicious subdomain that briefly existed.

Link : dns_sluth.zip

Sample: SPL{sone_random_text}

### Solution
The zip file provided contains 2 files: whois.txt and pdns.csv. whois.txt gives us the domain name ```secpen.org``` and pdns contains a list of subdomains along with other information in the format ```timestamp,subdomain,ip```. Looking through the ipv4 addresses, the first 2 octets all match as expected except for one ipv4 address. This ipv4 comming from a different network and its corrisponding suspicious subdomain, and the solution to this challenge.

## TrainEnc
### Description
A hostile comms channel emitted a fragmented payload before going silent. The payload appears scrambled and contains deliberate noise to confuse analysts. Intelligence believes the adversary used a transposition (or a variation) but added obfuscation so casual brute force won't immediately reveal the plaintext. Recover the hidden flag.

S96fP0226b9L7bcf40{64e5d403d74ad}
946ac55fa316df5b0671c5495795b23596eb

### Solution
From the title TrainEnc (likely hinting towards train encryption), and the intelligence information which predicts a transposition cipher was used, this challenge points to a rail-fence cipher. Since we also know this is a fragmented payload we can combine the two strings into one large one ```S96fP0226b9L7bcf40{64e5d403d74ad}946ac55fa316df5b0671c5495795b23596eb```. Lastely if we use the location of S and P to figure out the number of rails (10) we can generate a visual of the rail fence cipher used to encrypt the text.

```
S                 9                 6                 f              
 P               0 2               2 6               b 9             
  L             7   b             c   f             4   0            
   {           6     4           e     5           d     4           
    0         3       d         7       4         a       d         }
     9       4         6       a         c       5         5       f 
      a     3           1     6           d     f           5     b  
       0   6             7   1             c   5             4   9   
        5 7               9 5               b 2               3 5    
         9                 6                 e                 b
```

## mail mist
### Description 
The system has sent you a message, but something is not quite right.

Contact Support

### Solution
This challenge provides a website which has a textbox to input your email and send a message. Once you input your email you get an email saying ```Hello, BSides Noida is back with 0x03! Check out all the updates at https://bsidesnoida.in , Sometimes, a single comment on a website can reveal everything.``` The website itself and the email addresses arent helpful for finding the flag because its actually hidden within the email itself not the websites. If you download the original message you get a eml file which contains the ```X-CTF-Flag:``` with the flag present in plain text.

## bardeck
### Description
Rumors say the bartender hides something valuable behind the counter.

Task: Find the product name hidden in the bar.

Flag Format: SPL{random}

### Solution
This challenge contains one image with a barcode, and seemingly random code at the bottom. By copying down the value of the barcode and googling it you can quickly find the product referenced in the description. By inputting the product encapsulated in SPL{} you get the flag.

A little easter egg at the bottom is code written in Brainfuck, an esoteric programming language:
```
++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>++++++++++++.>---.+..+++++++.+++++++++++.<<++.>--------------.>------------------
-.+++++++++++++.-----------.++.<<.>>++++++++++.+++++++.-----------------.+++++++++++++.<<.>>++.------------.---.
<<.>++++++++++++++++.>+++++++++++++.<+++++++++++++.++++++++.>----.
```
when compiled it outputs ```Rabbit Dance over the Train```

## tv buzz
### Description
loves hiding things

Link: file.zip

Flag Sample: SPL{randomtext}

### Solution
The zip file provided contains one wav file which consists of nonsensical sounds which dont replicate a tv buzz as the title may suggest. With further inspection using audacity, switching from Waveform to Spectrogram reveals a hidden message containing the flag.
