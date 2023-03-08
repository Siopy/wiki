# 21 - FTP

## Enumeration

| Command                                                   | Description                                                             |
| --------------------------------------------------------- | ----------------------------------------------------------------------- |
| `ftp <FQDN/IP>`                                           | Interact with the FTP service on the target.                            |
| `nc -nv <FQDN/IP> 21`                                     | Interact with the FTP service on the target.                            |
| `telnet <FQDN/IP> 21`                                     | Interact with the FTP service on the target.                            |
| `openssl s_client -connect <FQDN/IP>:21 -starttls ftp`    | Interact with the FTP service on the target using encrypted connection. |
| `wget -m --no-passive ftp://anonymous:anonymous@<target>` | Download all available files on the target FTP server.                  |
| `ls -R`                                                   | Recursive list                                                          |

## Bruteforce FTP (Hydra / Medusa)



| Command                                                                     | Description      |
| --------------------------------------------------------------------------- | ---------------- |
| `medusa -u siopy -P /usr/share/wordlists/rockyou.txt -h 10.10.10.10 -M ftp` | Login Bruteforce |
| hydra -l user1 -P /usr/share/wordlists/rockyou.txt ftp://192.168.2.142      | Login Bruteforce |

