+++
title = "📱Babel"
description = "Real-time messaging and voice client in C++"
date = "2023-03-09"
extra.end_date = "2023-04-19"
extra.toc = true
+++

## [Repository](https://github.com/paulcomte/babel)

## Result

![Result](https://github.com/paulcomte/babel/raw/main/assets/preview.png)

## Introduction

### Project definition

This project was an `EPITECH` project, the project was defined as followed:

 - A client interface
 - TCP communication between the client and the server
 - UDP communication between two clients
 - Send messages to another client
 - Retrieve client conversation (messages sent and received)

### Tech stack
 - Programming language: C++
 - Window library: Qt
 - Server library: asio

### The journey

During this project I wanted to have lots of fun, and on top of the mandatory features, implement other features that to me, should be available on every real-time messaging and voice app.

Regarding the interface I decided to take the Discord interface for idea.

This was the first ever project where I started by working on the frontend, whereas my usual habit would be to work on the backend.

I wanted to have a clearer view of the result I wanted to provide, and also improve my frontend skills.

And actually, starting by working on the frontend was a good choice for two main reasons:

 - I did know in advance what features I would have on the client, so no time lost on the backend with unimplemented features on the client-side.
 - I lost a precious time trying to compile the frontend, so if I had to work on the frontend after the backend I might had not forseen this and I'd be unable to implement all features in time.

- ## Frontend architecture

> ### Scenes
 - #### Left layout
    - User: `Icon | Username | Logout`
    - Contact: `for contact in contacts => contactBox(contact)`
    - Search: `Text input`
 - #### Right layout
    - Chat info scene: `CallUp/HangUp Buttons`
    - Chat scene: `for message in messages => messageBox(message)`
    - Chat box scene: `Text input`

> ### Event system

The need for an event system was necessary the following interactions:

 - When the user would interact on the client, such as changing the selected contact, or looking for a contact by its name
 - When the server would send a packet to the client.

<br>

  - #### LOGIN_FAILED

| <u>**description**</u> |  errorMessage  |
| :--------------------: | :------------: | 
| <u>**field_type**</u>  |     string     |

  - #### LOGOUT

| <u>**description**</u> |     empty      |
| :--------------------: | :------------: | 
| <u>**field_type**</u>  |     empty      |

  - #### CONTACT_FILTER_UPDATE

| <u>**description**</u> |    newFilter   |
| :--------------------: | :------------: | 
| <u>**field_type**</u>  |     string     |
   
  - #### NEW_CONTACT

| <u>**description**</u> |      contact       |
| :--------------------: | :----------------: |
| <u>**field_type**</u>  | shared_ptr\<Client\> |

  - #### NEW_BULK_CONTACT

| <u>**description**</u> |          contacts          |
| :--------------------: | :------------------------: | 
| <u>**field_type**</u>  | vector\<shared_ptr\<Client\>\> |
 
  - #### NEW_MESSAGE

| <u>**description**</u> |        message        |
| :--------------------: | :-------------------: | 
| <u>**field_type**</u>  |  shared_ptr\<Message\>  |
 
  - #### NEW_BULK_MESSAGE

| <u>**description**</u> |            messages           |
| :--------------------: | :---------------------------: | 
| <u>**field_type**</u>  |  vector\<shared_ptr\<Message\>\>  |
 
  - #### NEW_CLIENT

| <u>**description**</u> |         client        |
| :--------------------: | :-------------------: | 
| <u>**field_type**</u>  |   shared_ptr\<Client\>  |
 
  - #### NEW_CHATTING

| <u>**description**</u> |         previousClient        |      newClient       |
| :--------------------: | :---------------------------: |:-------------------: |
| <u>**field_type**</u>  |     shared_ptr\<Client\>      |  shared_ptr\<Client\>  |
 
  - #### CALL_STATE_UPDATE
 
| <u>**description**</u> |       update       |
| :--------------------: | :----------------: |
| <u>**field_type**</u>  | shared_ptr\<Client\> |

## Backend architecture

> ### Database system

  - getMessages(string username) -> vector\<Message\>
  - getContacts(string username) -> vector\<string\>

> ### [Transporter](https://github.com/paulcomte/babel/blob/main/server/Transporter.hpp):

  Every conneted clients on the server has a `Transporter`, it implements the following functions:

  - sendMessage(string)
  - readMessage(function\<void(string) receivedMessage\> callback)
  - getHostname() -> string
  - close()
  - isClosed() -> bool

## Difficulties

In this project I encountered a major difficulty, which was with the compilation of the project on the linux distribution `NixOS`, I lost a lot of time.

I also faced another difficulty, that I sadly could not resolve, the audio library in C++ seems like to not work on Linux, therefore I can only compile the client on Windows if I enable the voice call feature...

## [Protocol system](/blog/a-protocol-system)

One of the fundamental point in this project was the protocol system.

It needed to be as flexible and ergonomic as possible.

I implemented a protocol system which I got so proud of that [I wrote an article](/blog/a-protocol-system) to explain how I proceedeed.

## Features

 - The icon of an user is automatically generated from his username.
 - Messages are stacked until `x` amount of time has passed, or `x` amount of messages has been sent.

## Limitations

Due to the limitations of my architecture, as it wasn't thought in time, and I didn't have time to refactor, the history of messages will only stack if the user switches to another conversation.

## Future?

If I ever get the chance to work on the project again, I would fix the previously cited limitation, and improve the abstraction, such as:

Instead of the following function: `getContacts(string username)`

> I would instead replace the `string` to an `Username` struct/class
