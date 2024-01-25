+++
title = "📱Babel"
description = "Real-time messaging and voice client in C++"
date = "2023-03-09"
extra.end_date = "2023-04-19"
extra.toc = true
+++

## Result

![Result](https://github.com/paulcomte/babel/raw/main/assets/preview.png)

## Project Definition

This project was an `EPITECH` project, the project was defined as followed:

 - A client interface
 - TCP communication between the client and the server
 - UDP communication between two clients
 - Send messages to another client
 - Retrieve client conversation (messages sent and received)

## Introduction

During this project I wanted to have lots of fun, and on top of the mandatory features, implement other features that should be necessary for every real-time messaging and voice app.

Regarding the interface I decided to take the Discord interface for idea.

## Tech stack
 - Programming language: C++
 - Window library: Qt
 - Server library: asio

## Difficulties

In this project I encountered a major difficulty, which was with the compilation of the project on the linux distribution `NixOS`, I lost a lot of time.

I also faced another difficulty, that I sadly could not resolve, the audio library in C++ seems like to not work on Linux, therefore I can only compile the client on Windows if I enable the voice call feature...

## Protocol system

One of the fundamental point in this project was the protocol system.

It needed to be as flexible and ergonomic as possible.

I implemented a protocol system which I got so proud of that I wrote an article to explain how I proceedeed, if you want more details, feel free to click [here](/blog/a-protocol-system).

## Features

 - The icon of an user is generated from his username
 - Messages are stacked until `x` amount of time has passed, or `x` amount of messages has been sent.

## Limitations

Due to the limitations of my architecture, as it wasn't thought in time, and I didn't have time to refactor, the history of messages will only stack if the user switches to another conversation.
