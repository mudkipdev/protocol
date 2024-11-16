# Teams
| Direction   | State | ID     | Identifier                  |
| ----------- | ----- | ------ | --------------------------- |
| Clientbound | Play  | `0x60` | `minecraft:set_player_team` |

This packet can be sent by the server to create, delete, or modify a scoreboard team. It is also used to add and remove players from a team.

## Fields
| Field  | Type   | Description          |
| ------ | ------ | -------------------- |
| Name | String | The team identifier. |
| Action | Byte | The [action](#actions) to perform on the team. |
| Data | [Action Data](#actions) | The parameters of the action. |

<details>
    <summary>Example Packet</summary>

| Field                      | Value   | 
| -------------------------- | ------- |
| Name | "`admins`" |
| Action | `0x03` |
| Members (length) | `2` |
| Member #1 | "`Notch`" |
| Member #2 | `e93a25ba-c1b4-4dfa-b161-9513c44c8ba9` |
</details>

## Actions
### Create Team (`0x00`)
| Field | Type | Description |
| ----- | ---- | ----------- |
| Display Name | Text | The user friendly name of the team. |
| Options | Byte | See [Options](#options). |
| Name Tag Visibility | String Enum | See [Name Tag Visibility](#name-tag-visibility). |
| Collision Rule | String Enum | See [Collision Rule](#collision-rule). |
| Color | VarInt Enum | The color and styling of player names on this team. |
| Prefix | Text | The text that is prepended to player names. |
| Suffix | Text | The text that is appended to player names. |
| Members | List of String | A list of entities in this team. The username is used for players and a UUID is used for entities. |

### Delete Team (`0x01`)
(no fields)

### Modify Team (`0x02`)
| Field | Type | Description |
| ----- | ---- | ----------- |
| Display Name | Text | The user friendly name of the team. |
| Options | Byte | See [Options](#options). |
| Name Tag Visibility | String Enum | See [Name Tag Visibility](#name-tag-visibility). |
| Collision Rule | String Enum | See [Collision Rule](#collision-rule). |
| Color | VarInt Enum | The color and styling of player names on this team. |
| Prefix | Text | The text that is prepended to player names. |
| Suffix | Text | The text that is appended to player names. |

### Join Team (`0x03`)
| Field | Type | Description |
| ----- | ---- | ----------- |
| Members | List of String | A list of entities that will join this team. The username is used for players and a UUID is used for entities. |

### Leave Team (`0x04`)
| Field | Type | Description |
| ----- | ---- | ----------- |
| Members | List of String | A list of entities that will leave this team. The username is used for players and a UUID is used for entities. |

## Options
A bit mask to control the client-side behavior of a team.

| Value | Bit | Description |
| ----- | --- | ----------- |
| Friendly Fire | `0x00` | Whether players on the same team can attack each other. |
| See Invisible Players | `0x01` | Whether players on the same team can see each other when they are invisible.

## Name Tag Visibility
A string enum that describes whether a player can see the name tag of someone on this team.

| Value | Description |
| ----- | ----------- |
| `always` | The player's name tag is visible to everyone. |
| `hideForOtherTeams` | Only others on the same team will be able to see the player's name tag. |
| `hideForOwnTeam` | Only people that are not on the player's team will be able to see the player's name tag. |
| `never` | No one can see this player's name tag. |

## Collision Rule
A string enum that describes whether a player on this team can collide with others.

| Value | Description |
| ----- | ----------- |
| `always` | This player collides with everyone. |
| `pushOtherTeams` | This player only collides with players on other teams. |
| `pushOwnTeam` | This player only collides with others on the same team. |
| `never` | This player does not collide with anyone. |