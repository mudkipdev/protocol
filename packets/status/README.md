# Status
This state is used to fetch server info and calculate network latency for the [server list](https://minecraft.wiki/w/Server_list).

## Table of Contents
### Clientbound
| ID (hex) | ID (decimal) | Name | Identifier |
| -------- | ------------ | ---- | ---------- |
| `0x00` | `0` | [Status Response](clientbound/000-status-response.md) | `minecraft:status_response` |
| `0x01` | `1` | [Ping](shared/001-ping.md) | `minecraft:keep_alive` |

### Serverbound
| ID (hex) | ID (decimal) | Name | Identifier |
| -------- | ------------ | ---- | ---------- |
| `0x00` | `0` | [Request Status](serverbound/000-request-status.md) | `minecraft:status_request` |
| `0x01` | `1` | [Ping](shared/001-ping.md) | `minecraft:keep_alive` |