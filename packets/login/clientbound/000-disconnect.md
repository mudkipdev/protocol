# Disconnect
| Direction   | State | ID     | Identifier                   |
| ----------- | ----- | ------ | ---------------------------- |
| Clientbound | Login | `0x00` | `minecraft:login_disconnect` |

Serves as the server's mechanism for terminating a connection during the login phase. It can be sent at any point during the login sequence, allowing servers to reject connections before they are fully established. When received, the client immediately closes the connection and displays the provided reason to the user.

## Fields
| Field  | Type | Description |
| ------ | ---- | ----------- |
| Reason | Text (JSON) | The reason displayed on the disconnect screen. |

## Usage
The reason field supports Minecraft's full text formatting system, allowing servers to provide rich, formatted text explaining the disconnection. Common scenarios include authentication failures, server maintenance, or version mismatches. Servers typically log these disconnect reasons for administrative purposes. Reasons may include:
* Invalid player name
* Server is full
* Authentication failure
* Incompatible client version
* Server maintenance

## Example
```json
{
    "text": "Server is restarting",
    "color": "red",
    "bold": true
}
```