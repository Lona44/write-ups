# Python Wrangling Writeup

![alt text](https://github.com/Lona44/write-ups/blob/main/PicoCTF/Python%20Wrangling/2021-05-10%2018_59_20-picoCTF%20-%20picoGym.png "Description")

Welcome to my writeup on the PicoCTF challenge, Python Wrangling! I'll be writing in a way that illustrates my train of thought as I first work my way through this exercise.

Above is a screenshot of the challenge we're given, including:
  * a python script called [`ende.py`](https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/ende.py)
  * an encrypted flag in a file called [`flag.txt.en`](https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/flag.txt.en)
  * a password in a file called [`pw.txt`](https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/pw.txt)

### Step 1: Getting the Files
Firstly, I note that in the `Submit Flag` text field, the format for any flags submitted is:
 * `picoCTF{ ... }`, where the flag we find is put between the curly brackets

We aren't given much else, so the first thing I do is pull the 3 files using `wget`
```bash
$ wget https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/ende.py
$ wget https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/flag.txt.en
$ wget https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/pw.txt
```

### Step 2: Having a Look at the Flag and Password Files
A quick check using `ls` should show the 3 files if we've managed to download them using step 1. We can have a look a the flag and password using `cat`:
```bash
$ cat flag.txt.en pw.txt
```
We see that the flag has a long value of `gAAAAABgUAIVI-r3OTKrDSgUJ8i3N9OzjacXZ1w4Hua00I_-Bg7gZu9Fld-TFYRiUiZlkLkChceqqpL9XnGOMO-W2-lRXpFhTkrqk9fHAvDfNkZHuZcjGPpG4xaR4mPnagzSNIrtL9tK` and the password value is `6008014f6008014f6008014f6008014f`.

### Step 3: Having a Look at the Python Code
We can use `Vim` to open up and have a look at the python file:
```bash
$ vim ende.py
```
We see the following:

![](https://github.com/Lona44/write-ups/blob/main/PicoCTF/Python%20Wrangling/ende_long_code.png "ende.py")

### Step 4: Making sense of the Python code
The first thing I notice in the code is that we import a Python package called `cryptography.fernet.Fernet`. To be honest, I can't remember if I've come across this package before, so I quickly have a look at the [documentation](https://cryptography.io/en/latest/fernet/), where we learn it uses symmetric key cryptography to encrypt and decrypt messages. I quickly skim through the documentation, just to give me an idea of how it's meant to work. I might need to come back to it later if I get stuck.

Heading back to the code, lines `8-12` are useful to understand the kind of command that'll properly execute the script. The example given on line `12` of correct formatting is:
```bash
$ python sys.argv[0] -d pole.txt
```
where `sys.argv[0]` represents the Python file we downloaded `ende.py`. We can also see the last arguement is a file that is to be decrypted. What does the `-d` flag do though? Scanning through the code, I see that lines `37-49` tell us that `-d` allows us to decrypt a given file. That must mean that the `-e` flag does the opposite and encrypts files, which we can verify by investigating the code block on lines `22-34`.

### Step 5: Breaking Down the Decryption Code Block
I need to know exactly how I'm going to use the decryption part of the code to get back a decrypted flag to submit. Investigating lines `37-49` further, it looks like we have two options to recover what we need:
  1. Only running the command from Step 3. with the `-d` flag and the file to decrypt. So `$ python ende.py -d flag.txt.en `. Line `39` tells us we'll get asked to enter a pssword, which we have and is contained in the `pw.txt` file we downloaded already.
  2. The other option is to enter everthing above, as well as appending the password as the last arguement. So if the password is say `password123`, then we'd run `$ python ende.py -d flag.txt.en password123`.

### Step 6: Recovering the Flag & Submitting
I like option 2 from the previous step. So I copy the password in the `pw.txt` to the clipboard, and enter the following and cross my fingers (note I'm using Python 3):
```bash
$ python3 ende.py -d flag.txt.en 6008014f6008014f6008014f6008014f
```
Thankfully, it worked! We get a flag back, which I'll let you work through to see ;)

### A Visual of How I See Everythihng Come Together
Below is the relevant code, along with how it connects to the various components of what we're given. Thanks for stopping by.
[](
