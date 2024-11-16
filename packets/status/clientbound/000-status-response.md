# Status Response
| Direction   | State      | ID     | Identifier            |
| ----------- | ---------- | ------ | --------------------- |
| Clientbound | Status     | `0x00` | `minecraft:status_response` |

This packet must be sent by the server after receiving a [Request Status](/packets/status/clientbound/000-status-response.md) packet.

## Fields
| Field | Type | Description |
| ----- | ---- | ----------- |
| Payload | String | The status payload encoded as a JSON string. |

## Payload
Here is an example of a status payload.

```json
{
    "version": {
        "name": "1.21.3",
        "protocol": 768
    },
    "players": {
        "max": 20,
        "online": 1,
        "sample": [
            {
                "name": "Notch",
                "id": "069a79f4-44e9-4726-a5be-fca90e38aaf5"
            }
        ]
    },
    "description": {
        "text": "A Minecraft Server"
    },
    "favicon": "data:image/png;base64,[png data goes here]",
    "enforcesSecureChat": false
}
```