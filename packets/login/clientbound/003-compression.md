# Compression
| Direction   | State | ID     | Identifier                    |
| ----------- | ----- | ------ | ----------------------------- |
| Clientbound | Login | `0x03` | `minecraft:login_compression` |

The compression packet configures the network compression settings for the entire connection. Once enabled, all subsequent packets follow a compressed format using zlib compression. This packet must be sent before the Login Success packet if compression is desired.

## Fields
| Field | Type | Description |
| ----- | ---- | ----------- |
| Threshold | VarInt | Maximum size of a packet before it is compressed |

## Compression Mechanics
When compression is enabled, packets larger than the specified threshold are compressed using zlib. The compression format adds a small overhead: a packet length field (VarInt) followed by the uncompressed data length (VarInt), and finally the compressed data itself. Packets smaller than the threshold are sent uncompressed to avoid unnecessary processing overhead. The choice of compression threshold significantly impacts server performance. A lower threshold results in more aggressive compression, reducing bandwidth usage at the cost of increased CPU usage. Higher thresholds reduce CPU overhead but may increase bandwidth consumption. Most vanilla servers use a threshold of 256 bytes as a balanced default.

## Common Threshold Values
* -1: Compression disabled entirely
* 0: All packets are compressed
* 256: Default vanilla server setting
* 512: Common for high-performance servers
* 1024: Minimal compression overhead