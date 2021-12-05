# Translation & Shifting

## Task 1
- This one is easy! We just need to read it!

```can you capture *** flag```

#### Task 2
- Looks like this is a binary! let translate to ASCII!

```lets *** some binary ****```

#### Task 3
- ```MJQXGZJTGIQGS4ZAON2XAZLSEBRW63LNN5XCA2LOEBBVIRRHOM======``` Looks like Base32 Encoding! Let decode!

```base32 is super common ** *****```

#### Task 4
- This looks like Base64 Encoding, Let decode!

```Each Base64 digit represents exactly 6 bits of data.```

#### Task 5
- Looks like this is a hex value!

```hexadecimal or ******?```

#### Task 6
- ROT13

```Rotate ** ** places!```

#### Task 7 
- ROT47

```You spin me right round baby right round *** ******```

#### Task 8
- Morse-Code

``` TELECOMMUNICATION ********```

#### Task 9
- Decimal

```Unpack this ***```

#### Task 10
- This one is a combination of things we saw before!
- I'll help a bit! ```Base64, Morse-Code, Binary, Rot47 and Decimal!```

```Let's make this a *** ********...```

# Spectrograms
- A spectrogram is a visual representation of the spectrum of frequencies of a signal as it varies with time. When applied to an audio signal, spectrograms are sometimes called sonographs, voiceprints, or voicegrams. When the data is represented in a 3D plot they may be called waterfalls. 

![****](/c4ptur3-th3-fl4g/Screenshots/Sonic.PNG)
![****](/c4ptur3-th3-fl4g/Screenshots/sonic2.PNG)

Boom!

# Steganography
- Steganography is the practice of concealing a file, message, image, or video within another file, message, image, or video.

- Command used:

```php
steghide extract -sf ./stegosteg.jpg
```
- Result
```php
Enter passphrase: 
wrote extracted data to "steganopayload2248.txt".
``` 
- For Passphrase leave it blank!

#### Our answer will be hidden in ```steganopayload2248.txt``` File
```Spag******teg```

# Security through obscurity
- Security through obscurity is the reliance in security engineering on the secrecy of the design or implementation as the main method of providing security for a system or component of a system.

#### Command I've used! ```strings``` which gets every string from the file we give it!

Here's the result

![****](/c4ptur3-th3-fl4g/Screenshots/obs.PNG)
