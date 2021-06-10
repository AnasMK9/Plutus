# Plutus Bitcoin Brute Forcer

A Bitcoin wallet collider that brute forces random wallet addresses
This repo is a fork of <a href="https://github.com/Isaacdelly/Plutus">Plutus</a>. The original program worked by generating a random private key on each iteration and looking up the address in the database. This fork tries a slightly different approach by generating a random private key and testing it alongside the next 10,000,000 private keys to find an address with balance. It also includes an updated database as of June 9th 2021.

# Like This Project? Give It A Star

[![](https://img.shields.io/github/stars/AnasMK9/Plutus.svg)](https://github.com/AnasMK9/Plutus.git)

# Dependencies

<a href="https://www.python.org/downloads/">Python 3.6</a> or higher

Python modules listed in the <a href="/requirements.txt">requirements.txt<a/>
  
Minimum <a href="#memory-consumption">RAM requirements</a>

# Installation

```
$ git clone https://github.com/AnasMK9/Plutus.git plutus

$ cd plutus && pip3 install -r requirements.txt
```

# Quick Start

```
$ python3 plutus.py
```

# Proof Of Concept

A private key is a secret number that allows Bitcoins to be spent. If a wallet has Bitcoins in it, then the private key will allow a person to control the wallet and spend whatever balance the wallet has. So this program attempts to find Bitcoin private keys that correlate to wallets with positive balances. However, because it is impossible to know which private keys control wallets with money and which private keys control empty wallets, we have to randomly look at every possible private key that exists and hope to find one that has a balance.

This program is essentially a brute forcing algorithm. It continuously generates random Bitcoin private keys, converts the private keys into their respective wallet addresses, then checks the balance of the addresses. If a wallet with a balance is found, then the private key, public key and wallet address are saved to the text file `plutus.txt` on the user's hard drive. The ultimate goal is to randomly find a wallet with a balance out of the 2<sup>160</sup> possible wallets in existence. 

# How It Works

Private keys are generated randomly to create a 32 byte hexidecimal string using the cryptographically secure `os.urandom()` function.

The private keys are converted into their respective public keys using the `starkbank-ecdsa` Python module. Then the public keys are converted into their Bitcoin wallet addresses using the `binascii` and `hashlib` standard libraries.

A pre-calculated database of every P2PKH Bitcoin address with a positive balance is included in this project. The generated address is searched within the database, and if it is found that the address has a balance, then the private key, public key and wallet address are saved to the text file `plutus.txt` on the user's hard drive.

This program also utilizes multiprocessing through the `multiprocessing.Process()` function in order to make concurrent calculations.

# Efficiency
#### Disclaimer: The effeceincy of this fork has not been tested yet.
It takes `0.0032457721` seconds for this progam to brute force a __single__ Bitcoin address. 

However, through `multiprocessing.Process()` a concurrent process is created for every CPU your computer has. So this program can brute force addresses at a speed of `0.0032457721 ÷ cpu_count()` seconds.

# Database FAQ

An offline database is used to find the balance of generated Bitcoin addresses. Visit <a href="/database/">/database</a> for information.

# Expected Output

Every time this program checks the balance of a generated address, it will print the result to the user. If an empty wallet is found, then the wallet address will be printed to the terminal. An example is:

>1Kz2CTvjzkZ3p2BQb5x5DX6GEoHX2jFS45

However, if a wallet with a balance is found, then all necessary information about the wallet will be saved to the text file `plutus.txt`. An example is:

>hex private key: 5A4F3F1CAB44848B2C2C515AE74E9CC487A9982C9DD695810230EA48B1DCEADD<br/>
>WIF private key: 5JW4RCAXDbocFLK9bxqw5cbQwuSn86fpbmz2HhT9nvKMTh68hjm<br/>
>public key: 04393B30BC950F358326062FF28D194A5B28751C1FF2562C02CA4DFB2A864DE63280CC140D0D540EA1A5711D1E519C842684F42445C41CB501B7EA00361699C320<br/>
>address: 1Kz2CTvjzkZ3p2BQb5x5DX6GEoHX2jFS45<br/>

# Memory Consumption

This program uses approximately 2GB of RAM per CPU. Because this program uses multiprocessing, some data gets shared between threads making it difficult to accurately measure RAM usage.

![Imgur](https://i.imgur.com/9Cq0yf3.png)

The memory consumption stack trace was made by using <a href="https://pypi.org/project/memory-profiler/">mprof</a> to monitor this program brute force 10,000 addresses on a 4 logical processor machine with 8GB of RAM. As a result, 4 child processes were created, each consuming 2100MiB of RAM (~2GB).

# Recent Improvements & TODO

- [X] Fixed typos/formatting

- [X] Update database

- [ ] Pickle loader

- [ ] Try to fix Memory Error

<a href="https://github.com/AnasMK9/Plutus/issues">Create an issue</a> so I can add more stuff to improve
# Buy me a coffee? 

    DOGE: DMBjr9hGLSydewmsA27ps3tR68gVBZwtvN
  <img src="https://user-images.githubusercontent.com/31940622/121449772-2276df00-c9a3-11eb-9915-61032c5a3201.png" width="300" height="300">

    BTC: bc1q7h8lzxrwqv4mm9s4nyfhuvzptpj4d9dk0wz7qs
  <img src="https://user-images.githubusercontent.com/31940622/121449800-2f93ce00-c9a3-11eb-8f58-6c554ab25f3e.png" width="300" height="300">
  
    BCH: qzqxznev0s30d8pu988p2lxkjsumty8qwqrtkdna3u
  <img src="https://user-images.githubusercontent.com/31940622/121449238-15a5bb80-c9a2-11eb-8615-6b2b48379e30.png" width="300" height="300">
  
    ETH: 0x1D6C2746E978ED8444B7f5e34e8bc747a1E8F1F7
  <img src="https://user-images.githubusercontent.com/31940622/121449262-1dfdf680-c9a2-11eb-830b-a2ac5c7c84be.png" width="300" height="300">
  
    LTC: ltc1ql0440qlhzhqatn99zk67mualrlpukggygy6hlv
  <img src="https://user-images.githubusercontent.com/31940622/121449299-3241f380-c9a2-11eb-94fd-eaaeba0ea90c.png" width="300" height="300">
