# 7) Schedule Backup (Cron)

Create a cron job that runs `/opt/backup.sh` every 2 minutes and archives `/etc`.

**Tasks**
1. Create the script:
   ```bash
   echo -e '#!/usr/bin/env bash\ntar -czf /tmp/etc_backup.tar.gz /etc' | sudo tee /opt/backup.sh
   sudo chmod +x /opt/backup.sh
   ```
2. Edit your user crontab:
   ```bash
   crontab -e
   # add the line:
   */2 * * * * /opt/backup.sh
   ```
3. Check logs to confirm cron runs:
   ```bash
   grep CRON /var/log/syslog | tail
   ```

**Goal**
Your crontab contains an entry for `/opt/backup.sh` every 2 minutes.
