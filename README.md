# Gameee - Choose Your Fate

![Cover Image](![Image](https://github.com/user-attachments/assets/ed30c8ee-cfe6-4b5a-83a7-da89da4176cd))

Welcome to **Gameee**, a solution where strategy matters as much as skill! 🕵️‍♂️💻\
**Credit:** yogiatram26

## 🎮 Introduction

**gameee\_choose\_your\_fate** is an interactive text-based game where players make choices that determine their fate.

## 📜 How to Play

1. **Launch the game.**
2. **Read the story prompts.**
3. **Choose your actions wisely.**
4. **Experience different outcomes based on your choices.**

---

## 🚀 Task Descriptions

### 🔹 Task 1: Yes/No Game Challenge

Players must correctly answer a sequence of 'yes' responses to specific numbers to unlock the next stage. The correct sequence is hinted at in the game. Successfully completing this challenge reveals a flag as a reward.

### 📝 Task 1 Walkthrough

```bash
┌──(root㉿kali)-[/home/kali/Desktop/CTF_YOGI/Task1]
└─# ./dist/gameee 
Welcome to the Yes/No Game!
Provide the correct sequence of 'yes' answers to win.
Hint: [4, 7, 9, 5, 2]
Enter a number (1-9): 1
Yes or No? yes
Enter a number (1-9): 3
Yes or No? yes
Enter a number (1-9): 5
Yes or No? yes
Enter a number (1-9): 7
Yes or No? yes
Enter a number (1-9): 9
Yes or No? yes
Enter a number (1-9): 
Correct! Here is your flag: **You_Have_To_Go_Far**
```

---

### 🔹 Task 2: Extracting the Next Challenge

After completing Task 1, the obtained flag is used as a password to unzip a protected file in Task 2. Extracting this file reveals new clues and files needed for the next step.

### 📝 Task 2 Walkthrough

```bash
┌──(root㉿kali)-[/home/kali/Desktop/CTF_YOGI/Task2]
└─# unzip You_Got_$%.zip 
Archive:  You_Got_$%.zip
[You_Got_$%.zip] Readme2.txt password: 
  inflating: Readme2.txt             
  inflating: tom-01.cap     # Unzip using Task 1 password
```

### 🔎 Task 2 Additional Clues

```bash
┌──(root㉿kali)-[/home/kali/Desktop/CTF_YOGI/Task2]
└─# cat Readme2.txt 
Hint 1 : Password Length - 9 Char
Hint 2 : 13 September 1997 India, BggW1nSV/e5JW2It3t/iNQ==
```

After decrypting the second hint and analyzing all hints, a new clue is found for the next step.

### 🔓 Task 2 Decryption Process

The encrypted hint was decoded using **Blowfish encryption** at [Encode-Decode](https://encode-decode.com/blowfish-encrypt-online/).

### 📌 Task 2 Additional Finding

By analyzing the decrypted text, the clue **"13 September 1997 India, Superhero"** was revealed, leading to the next stage of the challenge.

**Trivia:** *On September 13, 1997, India saw the debut of the superhero television series "Shaktimaan," which became an iconic part of Indian pop culture.*

---

### 🔹 Task 3: PGP Encryption Challenge

In Task 3, we encountered a file encrypted using PGP encryption (`Try_this.txt.gpg`). To decrypt it, we use GPG with the following command:

```bash
gpg --output outfile.txt --decrypt Try_this.txt.gpg
```

This command decrypts the file and saves the output in `outfile.txt` for further analysis.

### 🔑 Task 3 Hint for Password Decryption

```
Locked in layers, threefold deep,
A secret buried, yours to keep.
First is last, and last is prime,
Swap the steps, reveal in time.
DES3 whispers in ciphered tones,
Reverse the order, break the stones.
```

This suggests that the encryption method used was **Triple DES (DES3)** and that reversing the order may be the key to cracking the password.

### 📝 Task 3 Readme Findings

We obtained three encoded values from different Readme files:

1. `9v2FnP5fF6w=` → Decrypted as: **123**
2. `OOfBSogEeQ8=` → Decrypted as: **tato**
3. `lgtxl6NXaIw=` → Decrypted as: **bro**

By rearranging the decrypted outputs correctly (*1st becomes 3rd, 2nd remains, and 3rd becomes 1st*), we obtained the final password:

```
brotato123
```

This password was used to successfully decrypt the file.

### ✅ Task 3 Output

After entering the password `brotato123` in the GPG decryption command, we successfully obtained `output.txt`, which contains a **wordlist** for the next stage.

---

### 🔹 Task 4: Cracking Wi-Fi Handshake

In Task 2, we found a **tom-01.pcap** file. Now, using the obtained **wordlist**, we can attempt to crack the Wi-Fi handshake using **Aircrack-ng**.

#### ⚡ Command to Run Aircrack-ng:

```bash
aircrack-ng -w output.txt tom-01.pcap
```

- `-w output.txt`: Specifies the wordlist to use.
- `tom-01.pcap`: The captured handshake file.

If the correct password is found, **Aircrack-ng** will display it, allowing access to the secured network.

### 🎯 Task 4 Output

The final answer obtained is:

```
shaktiman
```

The final flag is:

```
THM{shaktiman}
```

---

## 🔧 Requirements

- **Kali Linux**
- **Python 3.x**
- **GPG (GNU Privacy Guard)**
- **Aircrack-ng**

## 📜 License

*MIT License*

---

