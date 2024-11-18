# Login Start (0x00)
| Direction   | State | ID     | Identifier        |
| ----------- | ----- | ------ | ---------------- |
| Serverbound | Login | `0x00` | `minecraft:hello` |

## Description
The Login Start packet initiates the login sequence from the client side. It contains the basic information needed to begin a connection: the player's username and UUID. This packet is sent immediately after transitioning from the handshake state to the login state.

## Fields
| Field | Type | Description |
| ----- | ---- | ----------- |
| Name | String (16) | Player's Username |
| Player UUID | UUID | The UUID of the player logging in. Unused by the Notchian server |

## Protocol Flow
When a client wishes to join a server, it first sends this packet containing the player's information. The server then determines how to proceed based on its configuration (online mode or offline mode) and the provided information. In online mode, this packet triggers the authentication process, while in offline mode, the server may proceed directly to completing the login sequence.

## Username Validation
The username field is limited to 16 characters and must match Minecraft's username requirements. These requirements include:
* 3-16 characters in length
* Alphanumeric characters and underscores only
* No spaces or special characters