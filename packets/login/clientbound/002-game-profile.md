# Game Profile
| Direction   | State | ID     | Identifier                |
| ----------- | ----- | ------ | ------------------------ |
| Clientbound | Login | `0x02` | `minecraft:game_profile` |

The Game Profile packet represents the final stage of the login sequence. When received, it signals to the client that authentication and encryption have been successfully established and the client can proceed to join the game world. This packet carries crucial information about the player's identity and appearance.

## Fields
| Field | Type | Description |
| ----- | ---- | ----------- |
| UUID | UUID | The player's unique identifier |
| Username | String (16) | The player's username |
| Properties | List of Property | |

## Properties System
The properties system primarily handles player appearance data, with the most important property being "textures." This property contains encoded information about the player's skin, cape (if any), and model type (classic or slim). These properties are cryptographically signed by Mojang to prevent tampering, ensuring that players cannot use unauthorized skins or capes.

| Field | Type | Description |
| ----- | ---- | ----------- |
| Property Name | Array of String (32767) | Property identifier (e.g., "textures") |
| Value | String (32767) | Property value (usually base64 encoded data) |
| Is Signed | Boolean | Whether the property is cryptographically signed |
| Signature | Optional String (32767) | Only if Is Signed is true |
| Strict Error Handling | Boolean | Whether the client should immediately disconnect upon a packet processing error |

## UUID System
The UUID system varies between online and offline mode servers. In online mode, UUIDs are version 3 (name-based) and remain consistent for premium accounts, allowing for persistent data storage and cross-server identification. Offline mode servers depending on implementation generate version 4 (random) UUIDs, which may change between sessions, or convert the players username to bytes to create a UUID.

## Temporary Error Handling
An addition in version 1.20.5 is the Strict Error Handling field. This temporary feature aids modded servers during the transition to the new data pack and registry system. When set to false, clients will silently ignore packet processing errors instead of disconnecting. This field is scheduled for removal in version 1.21.2.

## Example Property Data
```json
{
    "timestamp": 1627884800,
    "profileId": "...",
    "profileName": "Username",
    "textures": {
        "SKIN": {
            "url": "http://textures.minecraft.net/texture/..."
        },
        "CAPE": {
            "url": "http://textures.minecraft.net/texture/..."
        }
    }
}
```