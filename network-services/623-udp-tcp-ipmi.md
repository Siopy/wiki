# 623/UDP/TCP - IPMI

## Enumeration

| Command                                        |                         |
| ---------------------------------------------- | ----------------------- |
| `msf6 auxiliary(scanner/ipmi/ipmi_version)`    | IPMI version detection. |
| `msf6 auxiliary(scanner/ipmi/ipmi_dumphashes)` | Dump IPMI hashes.       |

## Bruteforce

| Command                                                  | Description                                           |
| -------------------------------------------------------- | ----------------------------------------------------- |
| `hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u` | Bruteforce IPMI 2.0 hashes (Hp iLo, default password) |
| `john --fork=8 --incremental:alpha -format=rakp true`    | Bruteforce (john version)                             |
