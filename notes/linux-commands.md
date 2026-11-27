# Linux & Security cheat sheet

## Git workflow (every time)
1. cd ~/cybersecurity-learning   - go to the repo
2. git pull                      - get the latest
3. nano journal/DATE.md          - write the journal
4. git add .                     - stage changes
5. git commit -m "Verb + what"   - save a version
6. git push                      - send to GitHub

## Navigation
- pwd            - where am I
- ls             - list files
- ls -la         - list all (hidden too) with permissions
- cd folder      - go into a folder
- cd ..          - go up one level
- cd ~           - go home
- cd /           - go to root
- .  = this folder   .. = parent   ~ = home   / = root
- Tab            - autocomplete names

## Files
- cat file               - show file content
- cp src dst             - copy
- mv old new             - rename or move
- mktemp -d              - make a random temp folder in /tmp
- file name              - file type (by first bytes, not name)
- rm -rf folder          - delete forever (ls first!)

## Search & text
- grep word file         - find lines with a word
- grep -v word file      - find lines WITHOUT a word
- grep -ri word .        - search all files (case-insensitive)
- cut -d',' -f4          - take column 4 (comma separated)
- sort                   - sort lines
- uniq -c                - count repeats (uniq is near-sighted: sort first!)
- sort | uniq -c | sort -nr  - count and rank
- strings file           - pull readable text from a binary
- Pipe |                 - send output to the next command

## Archives & encoding
- gzip -d f.gz           - unzip gzip
- bzip2 -d f.bz2         - unzip bzip2
- tar -xf f              - extract tar (then ls)
- xxd -r f > out         - hexdump back to a file
- base64 -d f            - decode base64 (encoding, NOT encryption)
- tr 'a-z' 'A-Z'         - replace characters (ROT13 etc.)

## Permissions & setuid
- r=4 w=2 x=1 ; owner group others ; e.g. 600 = owner read/write only
- chmod 600 file         - lock a key file
- chmod +x file          - make runnable
- s instead of x in ls -la = setuid (runs as the owner)
- ./bandit27-do cat FILE - run a command as the file's owner
- find / -perm -4000 2>/dev/null - find setuid files

## Processes
- ps -o pid,ppid,comm    - processes: id, parent, name
- ps -p N -o pid,ppid,comm - one process by id
- PID = which program, PPID = who started it
- follow PPID up to 1 = find who started everything

## Network & ports
- http 80, https 443, ssh 22 (Bandit uses 2220)
- nc -l -p 4444          - my server (Mac: nc -l 127.0.0.1 4444)
- nc host port           - connect to a port
- nmap -p 1-100 host     - scan ports
- nmap -sV -p 80,443 host - detect the service on each port
- lsof -i -P -n          - network connections on my Mac
- curl -I url            - response headers only
- curl -v url            - full request and response
- openssl s_client -connect host:port -quiet - TLS client

## SSH & keys
- ssh user@host -p port                 - log in
- ssh -i key user@host -p port          - log in with a key
- scp -P port user@host:file .          - copy a file from server (big P)
- ssh user@host -p port COMMAND         - run one command, no shell
- the prompt tells me where I am: ALBERT@MacBook = Mac, bandit@bandit = server

## Git history (secrets)
- git clone ssh://user@host:port/path   - clone a repo (from Mac use real host, not localhost)
- git log                               - commit history (q to quit)
- git show COMMIT                        - what changed (+ added, - removed)
- a password removed in a new commit STAYS in history -> rotate it
- cat /etc/passwd                        - users; last field = login shell

## Escape a restricted shell
- in more at --More-- press v  -> opens vi
- :set shell=/bin/bash  then  :shell  -> full terminal
- :r /path/file  - read a file onto the screen
- :q!  - quit without saving

## for loop & brute force
- for i in 1 2 3; do echo $i; done      - repeat for each item
- seq -w 0 9999                          - numbers 0000..9999
- cat attempts.txt | nc host port | grep -v Wrong - try all, keep the hit

## Windows logs (SOC)
- 4624 success logon, 4625 failed logon
- logon type: 2 keyboard, 3 network, 10 RDP
- brute force: many 4625 from one IP, then 4624 = password found
- 4688 process created (check the parent!)
- persistence: 7045 service, 4698 scheduled task, Run registry key
- 4720 user created, 4732 added to Administrators
- suspicious path: C:\Users\Public (normal programs live in System32)
