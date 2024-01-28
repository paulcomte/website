+++
title = "🐌 My stance on IDEs"
description = "I decided to use terminal editors instead of IDEs, even though they might sound complex, in the end, it was a great choice."

[taxonomies]
tags = ["thoughts", "development"]

[extra]
toc = true
+++

> IDE stands for `Integrated Development Evironment`

## The discovery

I started development around 2016, with the Java programming language, on a so-called "potato-pc".

I began by coding minecraft plugins, but I was **lost**, I learnt by watching tutorials, and on these tutorials, the developers were all using the `Eclipse` IDE, so I decided to do like them, and I gave this IDE a try.

The experience, was... **horrible**.

My computer, could barely handle the <u>*"heaviness"*</u> of the editor, and let's not talk about the compilation that was taking ages where I could not use my laptop at all anymore.

Also the IDE had many bugs with plugin development, the developers in the tutorials were saying that it was "normal", and that I'd get used to just ignoring the warnings and errors.

And so I did, for three months. I kept using `Eclipse`, I definetely lost hours through compilation, or by using the basic components of an IDE, such as going to the definition of a Java method, or implementing getters and setters.

## A way out?

And then. In 2017, I started watching anoher Minecraft developer, he was typing fast, his IDE looked great, and it looked like it was performant.

I proceeded to download `IntelliJ`.

And already, the bugs that `Eclipse` had, were no more. It was still slow on my computer, but it was a great progress, I could code faster.

But what made me fall in love with `IntelliJ` is the design, I never took the time to customize my `Eclipse` experience.

I had better performances, I had a nice background image on my code, the file icons looked great, thanks to the discovery of this new IDE, I definitely felt back in love with development, the spark rekindled.

## Entering University

I entered `EPITECH` in 2020, and during a whole month I did not use `IntelliJ` or any other IDEs.

We were learning the `C` programming language by reading `man` pages, and using `emacs`, having no `language server` installed.

*For those who don't know what a `language server` is, it's a tool bundled in IDEs that will act as a `middleware` between your code and the features of the language. Its simplest role can be of `syntax highlighting`, or also look for the use of variables, classes. etc*

Even though I had the features of a basic text editor, apart from `refactoring` my variables or structure names, I felt like I was coding faster than with an `IDE` running slowly on my computer.

I also didn't feel the need for any `file tree`.

## The relapse

Though, once I finished the month with the basic text editor, I installed `VSCode`, and felt a "relief".

## Hope?

In 2021, I learnt about the `vim` editor, I heard that "every cool dev", were using it.

So I decided to give it a try, but I felt like it was too hard, and not intuitive enough, so I gave up using it.

## Actual hope

Around 2022, I was getting really "linux-nerdy", I also wanted to use the lightest programs for everything, to save my laptop's battery, so instead of having only 3-4 hours of battery, I'd increase it to 6-7 hours.

I also became a big fan of the `Rust` programming language, and by looking for programs made in `Rust` on GitHub, I stumbled across `helix-editor`, a `vim` like editor, purely made in Rust.

I decided to give `vim` programs another shot. And I'm grateful that I did!

It was actuall way more intuitive than `vim`, and the `language servers` were already pre-installed.

*At the time of writing this post, `vim distros`, which install a version of `vim` with many bundled plugins, and language servers, are really famous, but I hadn't heard of any of them in 2022.*

So I stuck with it.

## Now?

To this day, `IntelliJ`, remains my favorite IDE, and the one that I will use whenever I'd do Java programming.

But by using the `helix-editor` *(which I'm currently writing the blog with)*, I feel like my laptop is thanking me, and that my development workflow became better, and way faster.

Especially on laptops, I feel like using the touchpad is a big loss of time, mouses on computers are still fine, but not having to move your hands at all, and keep your hands on your keyboard is an amazing thing.

## Recommendations

I don't recommend beginners in programming the use of editors like `vim`, they should learn the language itself first, and once they feel confident with it, they can use `helix-editor` or any `vim` distros.

And then, once they feel at ease with coding on `vim` they can fully customize it.

## Rust programming

Regarding the `Rust` programming language, there's currently `RustRover` made by `Jetbrains`, the creators of `IntelliJ`, in `Preview`, I used it for three good months, but I had to stop.

Even though I have a really good laptop nowadays, when using `RustRover` my computer lasts at most 2 hours, and is using 4-6GB of RAM just for the `IDE`, that's crazy.

I also tried out `lapce`, an editor made in `Rust`, and it's actually great! But it lacks stability, if you want to use it, please wait at least some months, maybe a year, until it becomes more stable.
