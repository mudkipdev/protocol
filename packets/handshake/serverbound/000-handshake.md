# Handshake
| Direction   | State      | ID     | Identifier            |
| ----------- | ---------- | ------ | --------------------- |
| Serverbound | Handshake  | `0x00` | `minecraft:intention` |

Sent by the client to let the server know that it is connecting.

> [!NOTE]
> The latest protocol version for Minecraft version 1.21.3 is `768`.

## Fields
| Field | Type | Description |
| ----- | ---- | ----------- |
| Protocol Version | VarInt | The networking version to determine client/server compatibility. |
| Server Address | String | The hostname or IP address used to connect. |
| Server Port | Short | The port used to connect. |
| Intention | VarInt | See [Intention](#intention). |

## Intention
An enum encoded as a VarInt. This represents the next state of the connection.

> [!WARNING]
> This enum starts its values at one instead of zero.

| Value  | Name | Description |
| -----  | ---- | ----------- |
| `0x01` | Status | Fetches server info to display on the [server list](https://minecraft.wiki/w/Server_list). |
| `0x02` | Login | Logs the player into the world. |
| `0x03` | Transfer | Another server has forwarded the player to this server. This can be treated the same as Login. |