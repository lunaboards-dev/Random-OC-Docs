# Tsukinet Reliable Communications (RC/TN), Version 1.0
Tsukinet's RC subprotocol is a synchronous, reliable stream protocol. Hint is 3.

## Packet format
| Field | Type | Notes |
| --- | --- | --- |
| Magic | 2 bytes | Always `RC` |
| Checksum | LE u24 |  |
| Identifier | 8 bytes | Randomly generated. |
| Port | LE u24 |  |
| Size | LE u16 |  |
