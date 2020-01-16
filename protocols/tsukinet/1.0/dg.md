# Tsukinet Datagram (DG/TK), Version 1.0
Tsukinet's Datagrams are a fast, unreliable, async subprotocol of TN. Hint is 2.

## Packet format
| Field | Type | Notes |
| --- | --- | --- |
| Magic | 2 bytes | Always `DG` |
| Port | LE u16 |  |
| Size | LE u16 | Datagrams are limited by the MTU. |
