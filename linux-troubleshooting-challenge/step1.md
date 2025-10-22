# 1) Exploring the System

Warm-up: collect basic information and commands.

**Tasks**
1. Print your working directory.
2. List files (long form) in `/etc` directory.
3. Show the last 10 lines of `/var/log/dpkg.log` (if missing, pick any log in `/var/log`).
4. If `ifconfig` and `route` are not available, install them: `sudo apt-get update && sudo apt-get install -y net-tools`. 
5. Save a summary to `/tmp/explore.txt` with at least:
   - your current directory
   - one network interface line
   - the default route (or lack thereof)
   - the kernel version (`uname -r`)

**Goal**
A file `/tmp/explore.txt` exists with the above information.
