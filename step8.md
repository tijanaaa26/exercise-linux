# 8) Disk Usage Mystery (deleted-but-open)

Sometimes disk is full even after deleting large files, because a process still holds them open.

**Tasks**
1. Demonstrate the problem (optional):
   ```bash
   dd if=/dev/zero of=/tmp/bigfile bs=1M count=64
   tail -f /tmp/bigfile >/dev/null &   # hold it open
   rm /tmp/bigfile
   ```
2. Find the culprit:
   ```bash
   sudo lsof | grep deleted | head
   ```
3. Fix by killing the process or truncating the FD (advanced).

**Goal**
You can identify a process that holds a deleted file (so `lsof` shows `deleted` entries).
