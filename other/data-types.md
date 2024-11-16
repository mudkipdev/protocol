# Data Types
Describes the most common data types in the Minecraft protocol.

| Name | Size | Description |
| ---- | ---- | ----------- |
| Optional T | 1 byte + size of T | A `true` value followed by T if it is present, otherwise `false`. |
| List of T | VarInt + length of sequence | A sequence of T prefixed by the list length as a VarInt. |
| Boolean | 1 byte | `true` is encoded as `0x01`, any other value is `false`.
| Byte | 1 byte | (Un)signed 8-bit integer. |
| Short | 2 bytes | (Un)signed 16-bit integer. |
| Integer | 4 bytes | (Un)signed 32-bit integer. |
| Long | 8 bytes | (Un)signed 64-bit integer. |
| Float | 4 bytes | Single-precision 32-bit [IEEE 754](https://en.wikipedia.org/wiki/IEEE_754) floating point number. |
| Double | 8 bytes | Double-precision 32-bit [IEEE 754](https://en.wikipedia.org/wiki/IEEE_754) floating point number. |
| UUID | 16 bytes | A 128-bit [universally unique identifier](https://en.wikipedia.org/wiki/Universally_unique_identifier). |
| String | - | A UTF-8 string prefixed by its size in bytes as a VarInt. Up to 32,767 characters long. |
| NBT | - | Minecraft's [custom binary format](https://minecraft.wiki/w/NBT_format).
| Text | - | An NBT or JSON encoded [text component](https://minecraft.wiki/w/Raw_JSON_text_format) value. |
| Identifier | - | [Resource location](https://minecraft.wiki/w/Resource_location) encoded as a string. |

> [!WARNING]
> This list is not complete. See the [wiki.vg](https://wiki.vg/Protocol#Data_types) page for more info.