# CVE-2020-1472
Checker & Exploit Code for CVE-2020-1472 aka Zerologon

Tests whether a domain controller is vulnerable to the Zerologon attack, if vulnerable, it will resets the Domain Controller's account password to an empty string.

NOTE: It will likely break things in production environments (eg. DNS functionality, communication with replication Domain Controllers, etc); target clients will then not be able to authenticate to the domain anymore, and they can only be re-synchronized through manual action.

Zerologon original research and whitepaper by Secura (Tom Tervoort) - https://www.secura.com/blog/zero-logon




https://user-images.githubusercontent.com/104816473/235369201-16c1eabd-4706-4589-bd31-de13fc414f86.mp4




# Exploit

It will attempt to perform the Netlogon authentication bypass. When a domain controller is patched, the detection script will give up after sending 2000 pairs of RPC calls, concluding that the target is not vulnerable (with a false negative chance of 0.04%).

The exploit will be successful only if the Domain Controller uses the password stored in Active Directory to validate the login attempt, rather than the one stored locally as, when changing a password in this way, it is only changed in the AD. The targeted system itself will still locally store its original password.

# Installation
## 1. Installtion as follows:
    1. git clone https://github.com/SecureAuthCorp/impacket
    2. cd impacket
    3. pwd ~/impacket/
    4. virtualenv --python=python3 impacket
    5. source impacket/bin/activate
    6. pip install --upgrade pip
    7. pip install
  
## 2. Install the Zerologon exploit script as follows:

    ~/impacket/
    cd examples
    git clone https://github.com/Akash7350/CVE-2020-1472/tree/main
    cd CVE-2020-1472
    pip install -r requirements.txt
# Example 
![image](https://user-images.githubusercontent.com/104816473/235366431-8f56bcfe-1516-4957-9f30-bb53c1de2300.png)
![image](https://user-images.githubusercontent.com/104816473/235366538-677baf7c-9acf-46c4-a5b0-b532c08dd800.png)
![image](https://user-images.githubusercontent.com/104816473/235366584-fd2b2ff9-80b7-4063-a637-d831883c2239.png)

# Research and Documentation 
https://www.secura.com/whitepapers/zerologon-whitepaper
https://github.com/Akash7350/CVE-2020-1472/blob/main/Report%20CVE%20CVE-2020-1472.pdf

