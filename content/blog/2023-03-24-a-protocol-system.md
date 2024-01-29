+++
title = "📡 A protocol system in C++"
description = "Creating a protocol system in C++ might seem not trivial at first, but actually is fairly pretty simple"
extra.toc = true

[taxonomies]
tags = ["cpp", "server", "communication"]
+++

## [Repository](https://github.com/paulcomte/babel/tree/main/protocol)

## Introduction

During the realization of the `Babel` project, I had to work on a protocol system, to enable interactions between the client and the server.

If you want more details about the base project, feel free to click [here](/projects/babel).

## Tech stack
 - Programming language: C++

> The protocol system does not depend on anything else.

## Architecture

> ### PacketManager

- #### Global functions

  - ##### deserialize(std::string &packet)
    ```
    1. message[0] == '0x32'?
       We check if the first byte is our magic value.

    2. PacketType = message[1]
       We retrieve the packet type from the next byte.

    3. PacketField[] = message[2..]
       We convert the rest of the content into a list of packet field.

    4. Packet = Deserialize(PacketType, PacketField[])
       We call the deserialize function for the specific packet type, with the list of packet fields.
    ```
  - ##### serialize(Packet&)

    > It will simply call the `serialize` inherited function from the Packet class.

- #### handlePacket(Packet &packet)
  - ##### [Server-side implementation](https://github.com/paulcomte/babel/blob/main/protocol/server/ServerPacketManager.cpp)
  - ##### [Client-side implementation](https://github.com/paulcomte/babel/blob/main/protocol/client/ClientPacketManager.cpp)

  A trivial implementation of the `handlePacket` function is to simply loop through all `PacketHandler`s, to target the one registered for the received packet.

  You can also use a `HashMap<PacketType, PacketHandler>`.

> ### PacketHandler

  - #### ServerPacketHandler
    ```
    handle(Packet&, std::shared_ptr<ServerManager>, IoClient*)
    ```

  - #### ClientPacketHandler
    ```
    handle(Packet&, std::shared_ptr<ClientManager>)
    ```

> ### Fields

<u>**Here's the base structure of a field**</u>

| <u>**description**</u> |  field_type   |       field       |
| :--------------------: | :-----------: | :---------------: |
|    <u>**size**</u>     |    1 byte     |  remaining bytes  |
|    <u>**value**</u>    |  0x00 => 0xFF |                   |

<br>

  - #### Character field
| <u>**description**</u> |  field_type   |      value     |
| :--------------------: | :-----------: |  :-----------: |
|    <u>**size**</u>     |    1 byte     |     1 byte     |
|    <u>**value**</u>    |     0x00      |  0x00 => 0xFF  |

  - #### Integer field (4 bytes)
| <u>**description**</u> |  field_type   |       [0]      |      [1]      |      [2]      |      [3]      |
| :--------------------: | :-----------: | :------------: | :-----------: | :-----------: | :-----------: | 
|    <u>**size**</u>     |    1 byte     |     1 byte     |     1 byte    |     1 byte    |     1 byte    |
|    <u>**value**</u>    |     0x01      |  0x00 => 0xFF  |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => 0xFF |

  - #### Unsigned Integer field (4 bytes)
| <u>**description**</u> |  field_type   |       [0]      |      [1]      |      [2]      |      [3]      |
| :--------------------: | :-----------: | :------------: | :-----------: | :-----------: | :-----------: | 
|    <u>**size**</u>     |    1 byte     |     1 byte     |     1 byte    |     1 byte    |     1 byte    |
|    <u>**value**</u>    |     0x02      |  0x00 => 0xFF  |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => 0xFF |

  - #### Unsigned Integer 64 field (8 bytes)
| <u>**description**</u> |  field_type   |       [0]      |      [1]      |      [2]      |      [3]      | [4] | [5] | [6] | [7] |
| :--------------------: | :-----------: | :------------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: | 
|    <u>**size**</u>     |    1 byte     |     1 byte     |    1 byte     |    1 byte     |     1 byte    |     1 byte    |     1 byte    |     1 byte      |     1 byte    |
|    <u>**value**</u>    |     0x03      |  0x00 => 0xFF  |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => OxFF |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => 0xFF |

  - #### String field
| <u>**description**</u> |  field_type   |    size[0]    |    size[1]    |    size[2]    |    size[3]    |      [0]      |     |      [n]      |
| :--------------------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: | :-: | :-----------: |
|    <u>**size**</u>     |    1 byte     |     1 byte    |     1 byte    |     1 byte    |     1 byte    |    1 byte     | n-1 bytes |   1 byte  |
|    <u>**value**</u>    |     0x04      |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => 0xFF | 0x00 => 0xFF |  0x00 => 0xFF |

> ### Packets

  <u>**Here's the base structure of a packet:**</u>

| <u>**description**</u> |   magic   |  packet_type  |      fields[]     |
| :--------------------: | :-------: | :-----------: | :---------------: |
|    <u>**size**</u>     |  1 byte   |    1 byte     |  remaining bytes  |
|    <u>**value**</u>    |   0x32    | 0x00 => 0xFF  |                   |

<br>

  - #### CallUpPacket
| <u>**description**</u> |    username    |    hostname    |      port      |
| :--------------------: | :------------: | :------------: | :------------: |
| <u>**field_type**</u>  |     string     |    string      |      uint      |

  - #### HangUpPacket
| <u>**description**</u> |    username    |
| :--------------------: | :------------: | 
| <u>**field_type**</u>  |     string     |

  - #### ContactPacket
| <u>**description**</u> |    username    |
| :--------------------: | :------------: | 
| <u>**field_type**</u>  |     string     |
  
  - #### LoginErrorPacket
| <u>**description**</u> |      error     |
| :--------------------: | :------------: | 
| <u>**field_type**</u>  |     string     |
  
  - #### LoginPacket
| <u>**description**</u> |    username    |
| :--------------------: | :------------: | 
| <u>**field_type**</u>  |     string     |
  
  - #### LogoutPacket
| <u>**description**</u> |     empty      |
| :--------------------: | :------------: | 
| <u>**field_type**</u>  |     empty      |
  
  - #### MessagePacket
| <u>**description**</u> |     sender     |    recipient   |     content    |    timestamp    |
| :--------------------: | :------------: | :------------: | :------------: | :-------------: | 
| <u>**field_type**</u>  |     string     |     string     |     string     |     uint64      |

## Sample implementation

You can check out the [GitHub wiki](https://github.com/paulcomte/babel/wiki) to have more details on an example implementation.

## Future ?

If I ever get the time to work on my protocol system, I would definitely write a file parser to create packets from simple json files.
