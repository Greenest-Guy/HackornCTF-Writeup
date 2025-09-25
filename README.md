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
The description consists of a message in hexidecimal (identifiable by pairs of numbers and letters) once decoded returns an encoded flag. Since we know the flag starts with SPL we can find the Unicode difference, from this difference we can find the offset. Using a simple ceasar cipher python script we can easily shift the flag values by the offset.
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
