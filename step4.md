# 4) Missing Log File (strace)

Our app prints an error but doesn't tell which file is failing.

**Tasks**
1. Create a tiny script that tries to append to `/var/log/app.log`:
   ```bash
   echo -e '#!/usr/bin/env bash\necho "$(date) started" >> /var/log/app.log' | tee /tmp/run_app.sh
   chmod +x /tmp/run_app.sh
   ```
2. Use `strace` to see open attempts and verify the missing file case:
   ```bash
   strace -e openat /tmp/run_app.sh 2>&1 | tail -n +1
   ```
3. Create the log file with safe permissions:
   ```bash
   sudo touch /var/log/app.log
   sudo chown root:adm /var/log/app.log
   sudo chmod 664 /var/log/app.log
   ```
4. Run again to confirm it now works.

**Goal**
`/var/log/app.log` exists and receives new lines.
