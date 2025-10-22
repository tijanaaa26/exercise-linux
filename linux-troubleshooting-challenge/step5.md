# 5) Interface & IP Setup

Bring an interface up and assign an IP.

**Tasks**
1. Identify a non-loopback interface name (e.g., `eth0`, `ens3`, etc.):
   ```bash
   ip link show
   ```
2. Bring it up (if down) and add IP `192.168.56.10/24`:
   ```bash
   sudo ip link set <iface> up
   sudo ip addr add 192.168.56.10/24 dev <iface>
   ```
   > If the address already exists on another interface, delete it first using `ip addr del`.
3. Show the address:
   ```bash
   ip -4 addr show dev <iface>
   ```

**Goal**
`ip -4 addr` shows `192.168.56.10/24` on your chosen interface.
