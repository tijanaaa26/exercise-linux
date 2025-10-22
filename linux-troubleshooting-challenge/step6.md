# 6) Default Route Check

Connectivity is broken because the default route is missing or wrong.

**Tasks**
1. Show current routes:
   ```bash
   ip route
   ```
2. Ensure the default route is set to `192.168.56.1` via your interface:
   ```bash
   sudo ip route replace default via 192.168.56.1
   ```
3. Verify:
   ```bash
   ip route | grep default
   ```

**Goal**
A default route `default via 192.168.56.1` is present.
