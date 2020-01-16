# Streams
Streams in Tsukinet have a standard procedure:
<ol>
  <li>Request socket
  <li>Open socket
  <li>Send data
  <li>Close socket
</ol>

In Lua, this would be done with:
```lua
local tn = require("tsukinet")
local sock = tn.tkrc(my_ip, port)
sock:write("lmao")
sock:close()
```

Under the hood, the library sends an empty RC/TN packet with the QUERY flag set. If it gets an empty RC/TN packet pack with the ACK flag set, the socket is established. If it's a NACK, it's not.

When not sending data, streams must be kept alive. This is done by sending a keepalive packet. Keepalive packets follow the format of the flags KEEPALIVE, NORESEND, NOCRC, and ASYNC being set, regardless of subprotocol. The content of the message is the time of the next keepalive message. If this is not understood, either use a specified timeout or the last time between keepalive messages, with tolerance.

Closing the socket sends an empty packet with the CLOSE flag set. There is no wait for the response.
