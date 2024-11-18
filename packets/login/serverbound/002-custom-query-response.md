# Custom Query Response
| Direction   | State | ID     | Identifier                      |
| ----------- | ----- | ------ | ------------------------------- |
| Serverbound | Login | `0x02` | `minecraft:custom_query_answer` |

The Custom Query Response packet is sent by clients in response to a Login Plugin Request from the server. It forms part of the extensible login sequence, allowing for custom handshaking processes beyond the standard Minecraft login flow. This system enables servers to implement additional verification or data collection steps during login.

## Fields
| Field | Type | Description |
| ----- | ---- | ----------- |
| Message ID | VarInt | Should match ID from server |
| Successful | Boolean | true if the client understood the request, false otherwise |
| Data | Optional List of Byte | Any data, depending on the channel |

## Response Behavior
When a client receives a plugin request, it must respond with this packet, regardless of whether it understands the request. The Message ID field must match the ID received in the request, allowing servers to correlate requests and responses. The Successful field indicates whether the client recognized and could process the plugin channel specified in the request.

## Data Handling
If the Successful field is false, no data payload is included in the response. If true, the client can include up to 1048576 bytes of channel-specific data. The format and content of this data depend entirely on the plugin channel being used, allowing for flexible custom protocols during the login sequence. The vanilla Minecraft client always responds with Successful set to false and no data payload, as it doesn't implement any custom login plugins. However, modded clients can implement handlers for specific channels, enabling additional functionality during login. Server implementations should be prepared to handle both successful and unsuccessful responses appropriately.

## Common Use Cases
This packet system is particularly valuable for:
* Mod compatibility verification
* Custom authentication systems
* Server network coordination
* Client configuration validation
* Resource pack management