# 2) Fix the Access

An app wants to write logs to `/opt/app/logs`, but it fails with `Permission denied`.

**Tasks**
1. Create the path and simulate the situation:
   ```bash
   sudo mkdir -p /opt/app/logs
   sudo adduser --system --no-create-home appuser || true
   sudo chown root:root /opt/app -R
   sudo chmod 755 /opt/app /opt/app/logs
   ```
2. Try to write as a non-privileged user to reproduce the issue:
   ```bash
   sudo -u nobody bash -c 'echo test > /opt/app/logs/app.log' || echo "fail (expected)"
   ```
3. Fix it **without** changing ownership of the whole `/opt/app`. You can:
   - change group ownership only for `/opt/app/logs`, or
   - set an ACL to allow writing for a specific user/group.

**Goal**
After your fix, the command below should succeed (no error):
```bash
sudo -u nobody bash -c 'echo ok > /opt/app/logs/app.log'
```
