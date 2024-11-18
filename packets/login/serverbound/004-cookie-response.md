# Cookie Response
| Direction   | State | ID     | Identifier                  |
| ----------- | ----- | ------ | --------------------------- |
| Serverbound | Login | `0x04` | `minecraft:cookie_response` |

The Cookie Response packet is sent by clients in response to a Cookie Request from the server. It provides a mechanism for transmitting stored cookie data back to the server during the login process. The Notchian server implements strict size limitations on these responses to prevent abuse.

## Fields
| Field | Type | Description |
| ----- | ---- | ----------- |
| Key | Identifier | The identifier of the cookie |
| Payload | Optional List of Byte | The data of the cookie. |

## Data Limitations
The Notchian server enforces a strict 5 kilobyte size limit on cookie response payloads. This limitation helps prevent potential abuse of the cookie system while still allowing sufficient space for typical session data. Server implementations should validate payload sizes to maintain consistency with vanilla behavior.

## Response Scenarios
The packet structure accommodates three possible scenarios:
* Cookie exists: Has Payload is true, followed by the cookie data
* Cookie doesn't exist: Has Payload is false, no additional fields
* Empty cookie: Has Payload is true, but Payload Length is 0

## Usage Patterns
Cookie responses typically contain session-related data such as:
* Previous server preferences
* User interface settings
* Authentication tokens
* Server network routing information
* Custom client configurations