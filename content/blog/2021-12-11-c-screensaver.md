+++
title = "🖥️ Implementing a screensaver in C"
description = "I implemented a screensaver in C with the CSFML graphical library"
extra.toc = true

[taxonomies]
tags = ["c", "graphics"]
+++

## [Repository](https://github.com/paulcomte/C-ScreenSaver)

## Introduction

While I was going back to my parents' home, I had 6 hours to kill in the train.

I had no internet nor any way to charge my laptop so I decided to work on something simple with libraries that my pc already had downloaded.

##  Items
 - A laptop with a linux environment installed (NixOS)
 - A charger with no power socket nearby
 - A C compiler (gcc)
 - A graphical library (SFML)

With that in mind I had an idea that seemed trivial and not too long to implement.

A `Screen saver` made in C

## Steps

I organized the project in the following small steps:

1. Initialize a simple window
2. Create an argument parser
2. Create a tick rate system
3. Implement a simple screen saver algorithm
