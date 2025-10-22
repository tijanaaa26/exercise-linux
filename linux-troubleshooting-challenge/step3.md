# 3) Broken Backup Service (systemd)

We want a service that archives `/etc` to `/tmp/etc_backup.tar.gz` when started.
The provided unit has an error.

**Tasks**
1. Create the script:
   ```bash
   echo -e '#!/usr/bin/env bash\ntar -czf /tmp/etc_backup.tar.gz /etc' | sudo tee /usr/local/bin/backup.sh
   sudo chmod +x /usr/local/bin/backup.sh
   ```
2. Create the **broken** unit file:
   ```bash
   sudo tee /etc/systemd/system/backup-agent.service >/dev/null <<'EOF'
   [Unit]
   Description=Backup Agent
   After=network.target

   [Service]
   Type=oneshot
   ExecStart=/usr/local/bin/backup.s  # <- typo on purpose
   RemainAfterExit=yes

   [Install]
   WantedBy=multi-user.target
   EOF
   ```
3. Try to start it and inspect errors:
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl start backup-agent || true
   sudo systemctl status backup-agent --no-pager
   ```
4. **Fix the unit** (`ExecStart` path), reload, enable and start:
   ```bash
   # fix file then
   sudo systemctl daemon-reload
   sudo systemctl enable --now backup-agent
   ```

**Goal**
Service is enabled and on start creates `/tmp/etc_backup.tar.gz`.
