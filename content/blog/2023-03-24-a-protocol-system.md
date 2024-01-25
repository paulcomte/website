+++
title = "📡 A protocol system in C++"
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

> ### Packet structure Here's the base structure of a packet:

| <u>**description**</u> |   magic   |  packet_type  |      fields[]     |
| :--------------------: | :-------: | :-----------: | :---------------: |
|    <u>**size**</u>     |  1 byte   |    1 byte     |  remaining bytes  |
|    <u>**value**</u>    |   0x32    | 0x00 => 0xFF  |                   |

> ### Field structure

| <u>**description**</u> |  field_type   |       field       |
| :--------------------: | :-----------: | :---------------: |
|    <u>**size**</u>     |    1 byte     |  remaining bytes  |
|    <u>**value**</u>    |  0x00 => 0xFF |                   |

> #### - Character field
| <u>**description**</u> |  field_type   |      value     |
| :--------------------: | :-----------: |  :-----------: |
|    <u>**size**</u>     |    1 byte     |     1 byte     |
|    <u>**value**</u>    |     0x00      |  0x00 => 0xFF  |

> #### - Integer field (4 bytes)
| <u>**description**</u> |  field_type   |       [0]      |      [1]      |      [2]      |      [3]      |
| :--------------------: | :-----------: | :------------: | :-----------: | :-----------: | :-----------: | 
|    <u>**size**</u>     |    1 byte     |     1 byte     |     1 byte    |     1 byte    |     1 byte    |
|    <u>**value**</u>    |     0x01      |  0x00 => 0xFF  |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => 0xFF |

> #### - Unsigned Integer field (4 bytes)
| <u>**description**</u> |  field_type   |       [0]      |      [1]      |      [2]      |      [3]      |
| :--------------------: | :-----------: | :------------: | :-----------: | :-----------: | :-----------: | 
|    <u>**size**</u>     |    1 byte     |     1 byte     |     1 byte    |     1 byte    |     1 byte    |
|    <u>**value**</u>    |     0x02      |  0x00 => 0xFF  |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => 0xFF |

> #### - Unsigned Integer 64 field (8 bytes)
| <u>**description**</u> |  field_type   |       [0]      |      [1]      |      [2]      |      [3]      | [4] | [5] | [6] | [7] |
| :--------------------: | :-----------: | :------------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: | 
|    <u>**size**</u>     |    1 byte     |     1 byte     |    1 byte     |    1 byte     |     1 byte    |     1 byte    |     1 byte    |     1 byte      |     1 byte    |
|    <u>**value**</u>    |     0x03      |  0x00 => 0xFF  |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => OxFF |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => 0xFF |

> #### - String field
| <u>**description**</u> |  field_type   |    size[0]    |    size[1]    |    size[2]    |    size[3]    |      [0]      |     |      [n]      |
| :--------------------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: | :-: | :-----------: |
|    <u>**size**</u>     |    1 byte     |     1 byte    |     1 byte    |     1 byte    |     1 byte    |    1 byte     | n-1 bytes |   1 byte  |
|    <u>**value**</u>    |     0x04      |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => 0xFF |  0x00 => 0xFF | 0x00 => 0xFF |  0x00 => 0xFF |

> ### PacketManager

This class contains two global functions:

- #### deserialize(std::string &packet):



- #### serialize(Packet &packet):

It will simply call the `serialize` inherited function from the Packet class.

- #### One-sided implementations

> ### Serialization & Deserialization
> ### Fields
> ### Packets

## Future ?

If I ever get the time to work on my protocol system, I would definitely write a file parser to create packets from simple json files
