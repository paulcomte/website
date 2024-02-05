+++
title = "🕹️ RqndomUHC"
description = "Create your Minecraft UHC plugins with ease."
date = "2021-09-03"
extra.end_date = "2023-06-01"
extra.toc = true
weight = 4
+++

## [Repository](https://github.com/paulcomte/RqndomUHC-API)

## Introduction

The idea of creating such Minecraft plugin's library, originated from the development of the [`RValue`](/blog/r-value) class in Java.

I had just finished working on my [`NarutoUHC`](/projects/naruto-uhc) Minecraft plugin, that I realized if I wanted to create more UHC plugins, I had to abstract the process as much as possible.

## Tech stack
 - Programming language: Java
 - Library: Spigot 1.16.5

## Developer's Documentation

I worked on a documentation made for developers who wanted to use this project to create their own UHC game modes.

You can find it [here](https://rqndomuhc.rqndomhax.io)

> Note: the documentation is still [`Work In Progress]`

## Project definition

The project is divided in two parts.

- Library: [**RqndomUHC-API**](https://github.com/paulcomte/RqndomUHC-API)

- Library implementation [**RqndomUHC**](https://github.com/paulcomte/RqndomUHC)

> Note: When I first started working on the project I had the idea of selling the `Library implementation`, and keeping the project closed-source

## Dependency injection

This is the **core-feature** of the library, allow dependency injection as much as possible, to push the Java's objet oriented programming to its limits.

Therefore, everything implemented, can be changed by other plugins implementing the library.

## Features

Here's a list of features available in the `RqndomUHC` plugin's library:
  - ### Worlds manager

  - ### Host config
 
  - ### Scoreboard
  
  - ### Dynamic inventories
  
  - ### Scoreboard
  
  - ### Player system
  
  - ### Task system
  
  - ### Message system

  - ### Role system

  - ### Events system
    There exists an event system, so other plugins could re-implement the events on the go.

  - ### Utils
    - Banners
      This utility help you create banners.
 
    - BukkitSerializer
      This serializer class can convert a List of `ItemStack` to a Base64 String, it's used in the plugin to store Inventories in a configuration file.

    - Chrono
      This static class converts a duration into a formatted value
    
    - FileManager
      This class lets you manage file configurations in `YAML` format.
    
    - HostConfig
      Configuration helper, that stores `RValue` data, and saves it into a configuration file.
    
    - HostItemStack
      An `ItemStack` (Minecraft items) that stores a `Consumer<PlayerInteractEvent`, to add event handlers to items on the go.

    - ItemBuilder
      Builder class to create a custom `ItemStack`.
    
    - PlayerUtils
      Utility class relative to the players:
        ```java
        double getRadius(Location, Location); // Returns a radius between two locations
        void clearInventory(Player); // Clears the Player's inventory
        void saveInventory(ItemStack[], Player, boolean clear); // Saves the player's inventory into the ItemStack, if clear is set to true, also clears the Player's inventory
        void giveInventory(ItemStack[], Player); // Sets the Player's inventory from the given ItemStack
        ```

  - ### RValue

## How to create a team system?

Your UHC plugins needs a team system? No problem, just follow me:

- Create a new team:

      class MonsterTeam implements Team {}

- ### A team system on a player's role:

  - Create a new role
  ```
  class Monster implements IRole {
      public Monster() {
        this.getValues().add("plugin_name.role.team", MonsterTeam.class);
      }
  }
  ```

  And that's it, now if you create a role that extends from `Monster`, it will automatically have the team `MonsterClass`
  
  - ### A team system on a player:
  ```
    GamePlayer gamePlayer; // This needs to be a valide GamePlayer
    gamePlayer.getValues().add("plugin_name.team", MonsterTeam.class)
  ```
