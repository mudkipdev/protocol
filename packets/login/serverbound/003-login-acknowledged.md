# Login Acknowledged
| Direction   | State | ID     | Identifier                    |
| ----------- | ----- | ------ | ---------------------------- |
| Serverbound | Login | `0x03` | `minecraft:login_acknowledged` |

The Login Acknowledged packet serves as the final step in the login sequence, sent by the client to confirm receipt of the Login Success packet. Upon sending this packet, the connection state transitions to configuration, marking the end of the login phase and the beginning of game configuration.

## Fields
This packet contains no fields, functioning purely as a state transition signal.

## Protocol Flow
When a client receives a Login Success packet, it processes the provided profile information and then sends this acknowledgment. The absence of fields in this packet emphasizes its role as a pure state transition marker. The server must wait for this acknowledgment before proceeding with the configuration phase of the connection.

## State Transition
The sending of this packet triggers several important changes in the connection:
* The login phase officially ends
* The configuration phase begins
* Both client and server prepare to handle configuration packets
* The connection becomes ready for game-specific data exchange

## Implementation Notes
Despite its simplicity, this packet plays a crucial role in maintaining proper connection state synchronization between client and server. Server implementations should ensure they don't send configuration packets until they receive this acknowledgment, as the client may not be ready to process them before completing the state transition.