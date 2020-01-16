# Tsukinet Address Resolution Protocol (ARP/TN), Vesion 1.0
This subprotocol has the hint value of `1`. This subprotocol's use is for helping with routing. This should almost always be shouted and is always async.

## Format
| Field | Type | Note |
| --- | --- | --- |
| Magic | 4 bytes | Always `arp:` |
| Size | 1 byte | Size of entire payload |
| Command | 1 byte | See below |
| Data | Raw data | |

## Commands
| Character | Command | Arguments | Notes |
| --- | --- | --- | --- |
| `!` | Advertise | None | Doesn't actually do anything, just serves to aid in matching TN addresses to hardware addresses. |
| `*` | Query | None | Dangerous on a large local network! May overload the computer. Responses are whispered advertisements. |
| `?` | Lookup | TN Address | Looks up the address. Response will be a whispered advertisement. |
| `>` | Claim address | TN Address | Claims the address. May not actually do anything on most local networks. Check with your local network administrator to see if they have a router in place. Check the flags of the no-op packet you get to see if it was successful. |
| `<` | Unclaim address | TN Address | Unclaims the address. See above. |
| `.` | Noop | None | Doesn't do anything. Can be used for (n)acks. |
