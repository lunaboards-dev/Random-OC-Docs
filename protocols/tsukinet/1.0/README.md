# Tsukinet, Version 1.0
Tsukinet is a networking stack for OpenComputers. It's theoretical MTU is 65335 KiB, but it is limited to approximately 8168 bytes in most cases.
The base protocol, refered to here as "TN".

## TN Address
The TN address is a 48-bit address with a 16-bit checksum. The entire address has four fields, the trunk, the branch, the leaf, and the checksum. The checksum is a CRC16 checksum of all bytes. Note: each binary field should be parsed as a little endian integer. Standard format for a Tsukinet address is `0000:0000:0000:169d`

### Local addresses
The `0000` trunk is for local addresses, though the `0000` branch can*not* be used, as this is where null addresses end up.

### Special addresses
Any addresses in the trunks over `efff` are considered "special" and, thus, are reserved.
`ffff:ffff` is full of special addresses which are functional.

### Broadcast addresses
There are three defined broadcast addresses:
* Global Broadcast Address (`ffff:ffff:ffff:ed74`)
* Global Maskable Broadcast Address (`ffff:ffff:fffe:f4ac`)
* Local Broadcast Address (`ffff:ffff:fffd:dec4`)

It should be noted that a router *should* block all three from being broadcast externally.

### Bridge trunks
There are a few bridge trunks, though some, if not all, may never go into use.
* `ffb0` - Minitel
* `ffb1` - GERT
* `ffbf` - IPv4

## TN Packet structure
| Field | Type | Notes |
| --- | --- | --- |
| Magic | 2 bytes | Should always be equal to `TK` |
| Version | 1 byte | Highest four bits are the major version, lower four are the minor. |
| Hint | 1 byte | Hint as to the subprotocol |
| Sender | TN Address | May be null in the case of an ARP address claim message. |
| Destination | TN Address | |
| Flags | Little endian unsigned 16-bit integer | See flags below |
| Message | Data | |

## TN Packet flags
Base flags:
* Sync (0x1)
* Async (0x2)
* Whisper (0x4)
* Shout (0x8)
* No Resend (0x10)
* No CRC (0x20)
* Acknowledged (0x40)
* Not acknowledged (0x80)
* LZSS (0x100)
* Query (0x200)
* Keepalive (0x400)
* Close (0x800)

### Loudness
Loudness tells how to respond to a packet, either with a broadcast, in the case of a datagram, or a send, in the case of a socket. Datagrams *may* be whispered.

### Sync vs Async
This is simply for a sanity check. Not much else.
