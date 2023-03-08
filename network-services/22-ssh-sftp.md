# 22 - SSH / SFTP

## Enumeration

| `ssh-audit.py <FQDN/IP>`                                    | Remote security audit against the target SSH service. |
| ----------------------------------------------------------- | ----------------------------------------------------- |
| `ssh <user>@<FQDN/IP>`                                      | Log in to the SSH server using the SSH client.        |
| `ssh -i private.key <user>@<FQDN/IP>`                       | Log in to the SSH server using private key.           |
| `ssh <user>@<FQDN/IP> -o PreferredAuthentications=password` | Enforce password-based authentication.                |

## Hunting SSH Key

`grep -rnw "PRIVATE KEY" /* 2>/dev/null | grep ":1"`

## Port forwarding

`ssh test@10.129.169.174 -L 5555:127.0.0.1:5555`
