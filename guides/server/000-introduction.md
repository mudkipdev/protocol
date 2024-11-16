# Introduction

> [!WARNING]
> This guide is under construction. Contributions are appreciated.

## Creating a TCP Server
1. Create a new project in your preferred language.
2. Listen for and accept TCP connections on port `25565`. Documentation in a few common languages are listed below.
   - Java: [`ServerSocket`](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/net/ServerSocket.html), the [Netty](https://netty.io) library is also frequently used.
   - Rust: [`TcpListener`](https://doc.rust-lang.org/std/net/struct.TcpListener.html)
   - Go: [`net.Listen`](https://pkg.go.dev/net#Listen)
   - Node.js: [`net.Server`](https://nodejs.org/api/net.html#class-netserver)
   - Python: [`socket`](https://docs.python.org/3/howto/sockets.html#creating-a-socket)
   - C++: no clue lol
3. Depending on the language you chose, there may be a library that does the boring work of packets for you. Whether or not you choose one is up to you.
4. Write a utility function to read [VarInts](/other/data-types.md#varint) from a buffer.
5. Write code to read and write packet frames from the connection.
    - Length (VarInt) - the size of the packet ID and data combined
    - ID (VarInt) - the ID of the packet
    - Data - the packet payload
6. Add code to look up packet IDs.
7. Make a system to encode/decode packets. The implementation of this is up to you.

## Handling Packets
1. Write a basic loop that will receive packets and look up their ID.
2. If the ID is `0x00`, read a [Handshake](/packets/handshake/serverbound/000-handshake.md) packet.
3. If the intent is set to `0x01`, transition the connection to the status state.
4. If the intent is set to `0x02` or `0x03`, transition the connection to the login state.