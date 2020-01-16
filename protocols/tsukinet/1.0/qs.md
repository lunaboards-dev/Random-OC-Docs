# Tsukinet Quick Sockets (QS/TN), Version 1.0
Tsukinet's Quick Sockets are unreliable, async sockets. Hint is 4.

## Packet format
| Field | Type | Notes |
| --- | --- | --- |
| Magic | 2 bytes | Always `QS` |
| Port | LE u16 |  |
| Size | LE u16 |  |
| Packet ID | u8 | Used to find the order of the messages, as they may arrive out of order. |
| Max ID | u8 |  |
