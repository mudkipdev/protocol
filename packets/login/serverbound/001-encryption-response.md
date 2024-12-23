# Encryption Response
| Direction   | State | ID     | Identifier      |
| ----------- | ----- | ------ | --------------- |
| Serverbound | Login | `0x01` | `minecraft:key` |

The Encryption Response packet is the client's reply to the server's Encryption Request during the login sequence. It contains the encrypted shared secret and verification token, establishing the basis for secure communication between client and server.

## Fields
| Field | Type | Description |
| ----- | ---- | ----------- |
| Shared Secret | List of Byte | The shared secret encrypted with the server's public key. |
| Verify Token | List of Byte | The verify token encrypted with the same public key as the shared secret. |

## Encryption Process
Upon receiving the server's public key and verify token in the Encryption Request packet, the client generates a random 16-byte shared secret. This secret, along with the verify token received from the server, is encrypted using the server's public key through RSA encryption. The encrypted values are then sent back to the server in this packet.

## Security Measures
The verify token serves as a challenge-response mechanism to prevent replay attacks. The server checks that the decrypted verify token matches the one it originally sent. This verification ensures that the client actually received and could respond to the encryption request, rather than replaying a captured packet. After this packet is sent and verified by the server, all further communication is encrypted using AES/CFB8 encryption with the shared secret as the key. This symmetric encryption provides efficient secure communication for the remainder of the session. In online mode, the server will also use this shared secret to verify the player's identity with Mojang's authentication servers.