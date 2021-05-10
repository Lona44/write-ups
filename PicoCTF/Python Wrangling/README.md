# Python Wrangling Writeup

![alt text](https://github.com/Lona44/write-ups/blob/main/PicoCTF/Python%20Wrangling/2021-05-10%2018_59_20-picoCTF%20-%20picoGym.png "Description")

Welcome to my writeup on the PicoCTF challenge, Python Wrangling! 

Above is a screenshot of the challenge we're given, including:
  * a python script called [`ende.py`](https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/ende.py)
  * an encrypted flag in a file called [`flag.txt.en`](https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/flag.txt.en)
  * a password in a file called [`pw.txt`](https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/pw.txt)

### Step 1. 
Firstly, note that in the `Submit Flag` text field, we see the format for any flags submitted. That is:
 * `picoCTF{ ... }`, where the flag we find is put between the curly brackets

We aren't given much else, so the first thing I do is pull the 3 files using `wget`
```bash
wget https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/ende.py
wget https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/flag.txt.en
wget https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/pw.txt
```

### Step 2.
A quick check using `ls` should show the 3 files if we've managed to download them using step 1. We can have a look a the flag and password using `cat`:
```bash
cat flag.txt.en pw.txt
```
We see that the flag has a long value of `gAAAAABgUAIVI-r3OTKrDSgUJ8i3N9OzjacXZ1w4Hua00I_-Bg7gZu9Fld-TFYRiUiZlkLkChceqqpL9XnGOMO-W2-lRXpFhTkrqk9fHAvDfNkZHuZcjGPpG4xaR4mPnagzSNIrtL9tK` and the password value is `6008014f6008014f6008014f6008014f`.

### Step 3.
We can use `Vim` to open up and have a look at the python file:
```bash
vim ende.py
```
