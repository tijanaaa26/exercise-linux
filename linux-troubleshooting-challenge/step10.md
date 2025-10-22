# 10) Mini HTTP Server

Expose a simple HTTP endpoint on port **7070** that returns `Hello trainee!`.

**Option A (ncat)**:
```bash
while true; do
  ncat -lk -p 7070 -c 'echo -e "HTTP/1.1 200 OK\r\n\r\nHello trainee!"'
done &
```

**Option B (python)**:
```bash
cat <<'PY' > /tmp/server.py
from http.server import BaseHTTPRequestHandler, HTTPServer
class H(BaseHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200); self.end_headers()
        self.wfile.write(b"Hello trainee!")
HTTPServer(('',7070), H).serve_forever()
PY
python3 /tmp/server.py &
```

Verify:
```bash
curl -s localhost:7070
```

**Goal**
`curl -s localhost:7070` prints `Hello trainee!`.
