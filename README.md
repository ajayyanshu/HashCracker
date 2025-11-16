# PyHashCracker ⚡

**PyHashCracker** is a high-performance, multi-threaded password recovery tool written in Python. It is inspired by features from professional tools like Hashcat, but built to be a clean, modern, and extensible Python project.

This tool is for educational purposes and ethical, authorized use only.

---

## 🚀 Features

* **⚡ Multi-Threaded:** Uses all available CPU cores (`multiprocessing`) to dramatically speed up cracking.
* **🎯 Multiple Attack Modes:**
    * **Brute-Force:** Standard character-by-character attack.
    * **Dictionary:** Tests millions of words from a wordlist.
    * **Rule-Based:** Smartly mutates dictionary words (`pass` -> `Pass!`, `P@ss123`, etc.) to find common patterns.
    * **Mask Attack:** Targeted brute-force for known patterns (e.g., `Admin?d?d?d`).
* **📊 Live Progress Bar:** A clean, real-time progress bar for all attack modes using `tqdm`.
* **⚙️ Professional CLI:** A user-friendly command-line interface built with Python's `argparse` module, complete with help menus.

---

## 🛠️ Installation

1.  Clone the repository:
    ```bash
    git clone [https://github.com/your-username/pyhashcracker.git](https://github.com/your-username/pyhashcracker.git)
    cd pyhashcracker
    ```

2.  Create a `requirements.txt` file with the following content:
    ```
    tqdm
    ```

3.  Install the required Python packages:
    ```bash
    pip install -r requirements.txt
    ```

---

## 📖 Usage

The script is run from the command line, with your target hash as the first argument. You must then choose one attack mode.

### 💬 Get Help

To see all available commands and options, use the `-h` flag:
```bash
python3 cracker.py -h
```
---
### 1. Brute-Force Attack (`-b`)
Checks all combinations of a given charset up to a max length.

```bash
# Example: Crack a 5-character, all-lowercase password
# Hash for 'hello' (sha256): 2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824
python3 cracker.py 2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824 \
    -a sha256 \
    -b \
    -c abcdefghijklmnopqrstuvwxyz \
    -l 5
```
### 2. Dictionary Attack (-d)
Tests every word from a given wordlist file (e.g., rockyou.txt).

```bash
# Example: Crack a password using a wordlist
# Hash for 'password' (md5): e10adc3949ba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824
python3 cracker.py e10adc3949ba59abbe56e057f20f883e \
    -a md5 \
    -d /path/to/rockyou.txt
```
### 3. Rule-Based Attack (-d + -r)
The most powerful attack. Applies a set of common mutations to every word in your dictionary.

```bash
# Example: Crack 'Password123' using the base word 'password'
# Hash for 'Password123' (sha1): c254b5505372b86f488583457016312b84781d05
python3 cracker.py c254b5505372b86f488583457016312b84781d05 \
    -a sha1 \
    -d /path/to/rockyou.txt \
    -r
```
### 4. Mask Attack
A highly-targeted brute-force. Use this when you know parts of the password.

Mask Syntax:

?l = Lowercase letter (a-z)

?u = Uppercase letter (A-Z)

?d = Digit (0-9)

?s = Special Symbol (!@#$%...)

Any other character is a literal.
