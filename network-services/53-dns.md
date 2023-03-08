# 53 - DNS

## Enumeration



| Command                               | Enumeration                              |
| ------------------------------------- | ---------------------------------------- |
| `dig ns <domain.tld> @<nameserver>`   | NS request to the specific nameserver.   |
| `dig any <domain.tld> @<nameserver>`  | ANY request to the specific nameserver.  |
| `dig axfr <domain.tld> @<nameserver>` | AXFR request to the specific nameserver. |
| `host support.d.com`                  | DNS lookup for the specified subdomain.  |

## Bruteforcing



| Command                                                                                                                                                                                                           | Description              |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| `dnsenum --dnsserver <nameserver> --enum -p 0 -s 0 -o found_subdomains.txt -f ~/subdomains.list <domain.tld>`                                                                                                     | Subdomain brute forcing. |
| `for sub in $(cat /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt);do dig $sub.site.com @10.129.14.128 \| grep -v ';\\|SOA' \| sed -r '/^\s*$/d' \| grep $sub \| tee -a subdomains.txt;done` | Subdomain brute forcing. |
| `dnsenum --dnsserver 10.129.81.128 -p 0 -s 0 -o found.txt -f /opt/useful/SecLists/Discovery/DNS/fierce-hostlist.txt sub.site.com`                                                                                 | Subdomain brute forcing. |
