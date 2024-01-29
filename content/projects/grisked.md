+++
title = "💸 Grisked"
description = "Manage your money efficiently"
date = "2022-09-15"
extra.end_date = "2023-01-18"
extra.toc = true
weight = 2
+++

## [Repository](https://github.com/Grisked)

## Result

![Grisked preview](/img/grisked.png)

## Introduction

Managing money is important, especially as a student where you have limited resources.

Using google sheets, or excel documents is not trivial, and might be tedious for beginners.

I heard about the app `Microsoft money`, but it was old, no longer supported on newer versions of Windows, so there came the idea to create a similar app by myself.

## Tech stack
 - Programming language: Rust
 - Window framework: iced.rs

## Architecture

- ### grisked_profile

  - #### Structures and Enums

    *Note: For fields with `#[serde(skip_serializing)]` above their declaration, they're not being serialized, therefore, not saved, as they're only fields for the `grisked_ui` runtime.*

    <details>
      <summary>enum BillType</summary>

      ```rust
      Income,
      Invoice,
      ```
    </details>
  
    <details>
      <summary>struct Bill</summary>

      ```rust
      bill_type: BillType,
      name: String,
      price: f64,
      due_date: u16,
      label_id: Option<usize>,
      ```
    </details>

    <details>
      <summary>struct Account</summary>

      ```rust
      name: String,
      #[serde(skip_serializing)]
      id: Option<usize>,
      default_balance: f64,
      bills: Vec<Bill>,
      color: [f32; 3],
      ```
    </details>

    <details>
      <summary>struct Currency</summary>

      ```rust
      symbol: char,
      name: String,
      alias: String,
      convert_rate: f32,
      ```
    </details>

    <details>
      <summary>struct Data</summary>

      ```rust
      #[serde(skip_serializing)]
      path: Option<String>,
      accounts: Vec<Acccount>,
      labels: Vec<Label>,
      #[serde(skip_serializing)]
      account_id: Option<usize>,
      ```
    </details>

    <details>
      <summary>struct Label</summary>

      ```rust
      id: usize,
      name: String,
      color: [f32; 3],
      ```
    </details>

    <details>
      <summary>struct Settings</summary>

      ```rust
      #[serde(skip_serializing)]
      path: Option<String>,
      currencies: Vec<Currency>,
      ```
    </details>

  - #### Serialization

    > Everything is serialized using the `json` format
    
    - ##### `settings.json`
      *This file stores global settings, not related to any account, you can view them as app settings*
    
    - ##### `data.json`
      *This file stores data related to the user, a list of accounts (themselves storing bills), and user-defined labels*

- ### grisked_ui

  - #### Event system definitions

    <details>
      <summary>enum UpdateBox</summary>

      ```rust
      LabelName(String),
      AccountName(String),
      InvoiceName(String),
      IncomeName(String),
      InvoiceAmount(String),
      IncomeAmount(String),
      AccountDefaultBalance(String),
      ```
    </details>

    <details>
      <summary>enum Message</summary>

      ```rust
      MenuChanged(MenuType),
      KeyPressed(KeyCode, Modifiers),
      PreviousAccount,
      NextAccount,
      SaveRequested,
      AddAccount,
      AddLabel,
      AddInvoice,
      AddIncome,
      UpdateBox(UpdateBox),
      ```
    </details>

  - #### Event system usage

    This event system was made for the user performing interactions on the app.
    The enum `Message` has self-explanatory members, such as when a user tries to click on the `NextAccount` arrow, or when he creates a new invoice, etc*

  - #### Menus
  
    <details>
      <summary>enum MenuType</summary>

      ```rust
      #[default]
      Dashboard,
      Accounts,
      AccountData(Account),
      Deadlines,
      Charts,
      Backup,
      ```
    </details>

## Difficulties

This project wasn't particulary difficult, or didn't have any complex issues, though implementing the UI style was really time-consuming.
