# HackornCTF 2025 Writeup

## sanity check
### Description
The Hackorn's ticketing system is compromised as the organizers announced.

Update: announcement tab is hiding some secret, reveal to see through. #PlainSight

### Solution

In the Hackor[n] discord announcements tab there is a hidden flag within the first message sent inside that channel.

## the easy flag
### Description
Slippery snakes swiftly slide, seekers seek sly secrets stashed, flag flickers fast.. find it first!

Link to file : easychallenge.py

Ref: SPL{some_random_text}

### Solution

Running the Python file given in the challenge prints to the terminal the flag once wrapped in SPL{}

## EncTy
### Description
51 4E 4A 7B 7A 39 32 39 39 64 31 79 30 31 38 35 32 39 36 31 61 7A 79 63 31 31 39 79 30 35 32 63 39 36 79 79 37 35 33 32 38 32 63 31 36 63 31 64 35 79 37 39 61 34 30 35 31 7A 63 30 32 32 30 39 38 38 38 33 7D

### Solution
The description consists of a hexidecimal string once decoded returns QNJ{z9299d1y01852961azyc119y052c96yy753282c16c1d5y79a4051zc022098883}. Since we know the flag starts with SPL seeing that this output starts with QNJ, we know the hex values are offset by 2. Using a ceasar cipher script I created, you can shift the output into the correct flag.
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
