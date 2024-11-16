# Ping
| Direction   | State      | ID     | Identifier             |
| ----------- | ---------- | ------ | ---------------------- |
| Both        | Status     | `0x01` | `minecraft:keep_alive` |

When this packet is sent, the other side must respond with the same timestamp.

## Fields
| Field  | Type   | Description          |
| ------ | ------ | -------------------- |
| Timestamp | Long  | The Unix time in milliseconds this packet was sent at. |