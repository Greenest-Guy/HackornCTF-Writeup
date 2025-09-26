# HackornCTF Quals 2025 Writeup
```
 __    __                      __                                       ______   ________  ________ 
/  |  /  |                    /  |                                     /      \ /        |/        |
$$ |  $$ |  ______    _______ $$ |   __   ______    ______   _______  /$$$$$$  |$$$$$$$$/ $$$$$$$$/
$$ |__$$ | /      \  /       |$$ |  /  | /      \  /      \ /       \ $$ |  $$/    $$ |   $$ |__
$$    $$ | $$$$$$  |/$$$$$$$/ $$ |_/$$/ /$$$$$$  |/$$$$$$  |$$$$$$$  |$$ |         $$ |   $$    |
$$$$$$$$ | /    $$ |$$ |      $$   $$<  $$ |  $$ |$$ |  $$/ $$ |  $$ |$$ |   __    $$ |   $$$$$/
$$ |  $$ |/$$$$$$$ |$$ \_____ $$$$$$  \ $$ \__$$ |$$ |      $$ |  $$ |$$ \__/  |   $$ |   $$ |
$$ |  $$ |$$    $$ |$$       |$$ | $$  |$$    $$/ $$ |      $$ |  $$ |$$    $$/    $$ |   $$ |
$$/   $$/  $$$$$$$/  $$$$$$$/ $$/   $$/  $$$$$$/  $$/       $$/   $$/  $$$$$$/     $$/    $$/
```

This repository contains my personal solutions for challenges in the HackornCTF Quals 2025 competition. 

**Skills**
- Cryptography & Cipher Analysis
- Audio Steganography & Spectrogram Analysis
- Python Automation & Decoding
- Kali Linux Command Line tools
- Digital Forensics
- Open-Source Intelligence


## sanity check
**Category:** MISC

**Files/Links Provided:** N/A

**Description:**  

```
The Hackorn's ticketing system is compromised as the organizers announced.
Update: announcement tab is hiding some secret, reveal to see through. #PlainSight

    Flag sample : SPL{some_random_text}
```

**Steps to Solve:**  
1. Locate and join the Hackor[n] Discord server.
2. Navigate to the announcements tab.
3. Reveal the hidden flag in the first message by clicking the spoiler text.



## the easy flag
**Category:** MISC

**Files/Links Provided:** ```easychallenge.py```

**Description:**  

```
Slippery snakes swiftly slide, seekers seek sly secrets stashed, flag flickers fast.. find it first!

Link to file : easychallenge.py

Ref: SPL{some_random_text}
```

**Steps to Solve:**  
1. Download the ```easychallenge.py``` file to your computer.
2. Run the Python code inside of Visual Studio Code.
3. Copy the flag printed to the terminal.




## tv buzz
**Category:** MISC

**Files/Links Provided:** ```file.zip``` -> (```weird_radio.wav```)


**Description:**  

```
loves hiding things

Link: file.zip

Flag Sample: SPL{randomtext}
```

**Steps to Solve:**  
1. Download file.zip.
2. Extract the contents of file.zip.
3. Analyze the WAV file within Audacity.
4. Convert the view from Waveform to Spectrogram.
5. Transcribe the hidden text from the Spectrogram to reconstruct the flag (switching flag to SPL).

**Code / Commands / Images**
![image](https://github.com/Greenest-Guy/HackornCTF-Writeup/blob/main/images/Spectrogram.png)



## mail mist
**Category:** MISC

**Files/Links Provided:** ```Contact Support```

**Description:**  

```
The system has sent you a message, but something is not quite right.

Contact Support
```

**Steps to Solve:**  
1. Open the ```Contact Support``` link in a new tab.
2. Input an email address and click ```Send Mail```.
3. Open your inbox and locate the email.
4. Download the email's ```Original Message```.
5. Search for ```SPL``` and locate the flag under ```X-CTF-Flag```.

**Code / Commands / Images**

![image](https://github.com/Greenest-Guy/HackornCTF-Writeup/blob/main/images/mail_mist.png)



## copy paste
**Category:** Threat Intel L1

**Files/Links Provided:** ```copy_paste.zip``` -> (```server log для deepseek 2.txt```)

**Description:**  

```
Attackers often test or leak credentials on public paste sites. Can you find the leaked credential?

Link: copy_paste.zip

Sample: SPL{some_random_text}
```

**Steps to Solve:**  
1. Download and extract ```copy_paste.zip```.
2. Open the extracted text file within a text editor.
3. Using ```Ctrl+F``` search for a plaintext username & password.
4. Reconstruct the flag using SPL{username_password}.



## dns sluth
**Category:** Threat Intel L1

**Files/Links Provided:** ```dns_sluth.zip``` -> (```pdns.csv```, ```whois.txt```)

**Max Attempts:** 3

**Description:**  

```
A suspicious phishing email claimed to come from support-hackorn.secpen.org - as reported. Goal: Identify the suspicious subdomain that briefly existed.

Link : dns_sluth.zip

Sample: SPL{sone_random_text}
```

**Steps to Solve:**  
1. Download and extract ```dns_sluth.zip```.
2. Open ```pdns.csv``` in VSCode (timestamp,subdomain,ip).
3. Take note of the first 2 octets that are common between the IPv4 addresses (same network).
4. Locate the IP with a suspicious IPv4 address (first 2 octets different).
5. Find the subdomain associated with suspicious IPv4 address using the csv file.
6. Reconstruct the flag using the suspicious subdomain (SPL{subdomain}).



## mal medium
**Category:** Threat Intel L1

**Files/Links Provided:** ```mal_medium.zip``` -> (```network.log```, ```pastebin.txt```, ```strings.txt```, ```vt_reports.json```)

**Max Attempts:** 3

**Description:**  

```
Can you trace the infection path and identify the C2 domain?

Source: mal_medium.zip
```

**Steps to Solve:**  
1. Download and extract ```mal_medium.zip```.
2. Open pastebin.txt within a text editor and look for an abnormal string.
3. Inspect the string and decode it from Base64.
4. Locate the C2 domain from the decoded message.
5. reconstruct the flag with SPL{C2_Domain}.

**Code / Commands / Images**

```bash
Base64 -d file.txt
```



## EncTy
**Category:** CRYPTO

**Description:**  

```
51 4E 4A 7B 7A 39 32 39 39 64 31 79 30 31 38 35 32 39 36 31 61 7A 79 63 31 31 39 79 30 35 32 63 39 36 79 79 37 35 33 32 38 32 63 31 36 63 31 64 35 79 37 39 61 34 30 35 31 7A 63 30 32 32 30 39 38 38 38 33 7D
```

**Steps to Solve:**  
1. Copy the hexadecimal message presented in the description.
2. Create a Python function to decode a hexadecimal string.
3. Find the shift between the first three letters of the decoded string to SPL (ex. EFG -> ABC = -4)
4. Use a Python script to decode the message as a Ceasar cipher using the calculated shift.
5. Reconstruct the flag into the format SPL{}.

**Code / Commands / Images**

```python
def decode_hex(hex):
    return bytes.fromhex(hex).decode('utf-8')
```

```python
def decrypt_ceasar(text, key):
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



## TrainEnc
**Category:** CRYPTO

**Description:**  

```
A hostile comms channel emitted a fragmented payload before going silent. The payload appears scrambled and contains deliberate noise to confuse analysts. Intelligence believes the adversary used a transposition (or a variation) but added obfuscation so casual brute force won't immediately reveal the plaintext. Recover the hidden flag.

S96fP0226b9L7bcf40{64e5d403d74ad}

946ac55fa316df5b0671c5495795b23596eb
```

**Steps to Solve:**  
1. Copy the payloads into VSCode.
2. Concatonate the fragmented payload into one.
3. Calculate the num rails to reconstruct SPL in a Rail fence cipher by using spaces between (align S and P).
4. Construct the rail fence.
5. Transcribe it following the wave to reconstruct the flag.

**Code / Commands / Images**

`num_spaces = 2*(num_rails-2) + 1`

```
S                 9                 x                 f              
 P               0 2               x x               b 9             
  L             7   b             x   x             4   0            
   {           6     4           x     x           d     4           
    0         3       d         7       4         a       d         }
     9       4         6       a         c       5         5       f 
      a     3           1     6           d     f           5     b  
       0   6             7   1             c   5             4   9   
        5 7               9 5               b 2               3 5    
         9                 6                 e                 b
```


## SwArmy
**Category:** CRYPTO

**Description:**  

```
Sigurd Petter Ludvig { Sexa Trea Nolla Caesar Tvåa Filip Ett Caesar Nolla Erik Erik Ett Bertil Åtta David Sju David Adam Femma Sju Caesar Filip Åtta Nia Trea Sexa Adam Erik Sju Erik Sju Åtta Tvåa Sju Fyra Adam Bertil Adam Nolla Bertil Filip David Sju Sexa Femma Filip Erik Ett Nolla Adam Tvåa Nolla David Filip Erik Femma Åtta Nolla Filip Nia Erik Erik Caesar Caesar }
```

**Steps to Solve:**  
1. Copy the description into VSCode.
2. Translate Swedish words into their corresponding numbers (ex. Åtta -> 8)
3. Create a Python script to take the first letter from each word and concatenate them into one string, thus reconstructing the flag.

**Code / Commands / Images**

```python
message = "S P L { test message 6 7 }"

for i in message.split(" "):
    print(i[0], end='')
```



## bardeck
**Category:** OSINT

**Files/Links Provided:** ```OSINT-.pdf```

**Description:**  

```
Rumors say the bartender hides something valuable behind the counter.

Task: Find the product name hidden in the bar.

Flag Format: SPL{random}
```

**Steps to Solve:**  
1. Download and open ```OSINT-.pdf```
2. Transcribe the barcode number in the PDF.
3. Google the barcode number to find its corresponding product.
4. Construct the flag using the product name with no capital letters or spaces.

**Code / Commands / Images**

```brainfuck
++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>++++++++++++.>---.+..+++++++.+++++++++++.<<++.>--------------.>------------------
-.+++++++++++++.-----------.++.<<.>>++++++++++.+++++++.-----------------.+++++++++++++.<<.>>++.------------.---.
<<.>++++++++++++++++.>+++++++++++++.<+++++++++++++.++++++++.>----.
```
A hidden Easter egg in this challenge is a Brainfuck program which prints ```Rabbit Dance over the Train``` when compiled!\



## FileNOM
**Category:** Forensics

**Files/Links Provided:** ```BSN.wav```, ```BSO.wav```

**Max Attempts:** 2

**Description:**  

```
Listen Instruction Carefully !

Every artifact leaves behind a trace.. but only when handled with precision can the true evidence be uncovered. Investigators often rely on maintaining a flawless chain of custody to preserve hidden truths.

Your task is to analyze the provided audio file. But don’t expect it to be obvious.. no simple playback will help you here.

Think like a forensic examiner: preserve, observe, and extract without corruption.
```

**Steps to Solve:**  
1. Download both ```BSN.wav```, and ```BSO.wav```.
2. Open both together within Audacity.
3. Switch the view from Waveform to Spectrogram.
4. Expand BSO.wav vertically to uncover a hidden flag.
5. Transcribe the hidden flag into the SPL{} format.
