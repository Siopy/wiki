# Hunting

## Hunting for Files

`for ext in $(echo ".xls .xls* .xltx .csv .od* .doc .doc* .pdf .pot .pot* .pp*");do echo -e "\nFile extension: " $ext; find / -name *$ext 2>/dev/null | grep -v "lib|fonts|share|core" ;done`

## Find files of user/group (without errors)

`find / 2>/dev/null -user toto`

`find / 2>/dev/null -group mygroup`
