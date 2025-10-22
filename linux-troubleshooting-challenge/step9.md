# 9) User Stats Script

Write a script that prints three lines with counts.

**Tasks**
Create `/usr/local/bin/check_users.sh` that prints exactly:

```
USERS_UID_GT_1000=<number>
USERS_WITH_HOME=<number>
USERS_WITH_BASH=<number>
```

**Hints**
- Use `/etc/passwd`
- UID is the 3rd field
- Home dir is 6th field (exists on disk)
- Shell is 7th field

Example skeleton:
```bash
#!/usr/bin/env bash
gt1000=$(awk -F: '$3>1000{c++} END{print c+0}' /etc/passwd)
withhome=$(awk -F: '{ if (system("test -d "$6) == 0) c++ } END { print c+0 }' /etc/passwd)
withbash=$(awk -F: '$7~/\/bin\/bash/{c++} END{print c+0}' /etc/passwd)

echo "USERS_UID_GT_1000=$gt1000"
echo "USERS_WITH_HOME=$withhome"
echo "USERS_WITH_BASH=$withbash"
```
Make it executable: `sudo chmod +x /usr/local/bin/check_users.sh`

**Goal**
Running `/usr/local/bin/check_users.sh` prints 3 lines as specified.
