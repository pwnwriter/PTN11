---
title: "OS as Code: Using Nix on Apple Silicon and More"
author: Nabeen Tiwaree (pwnwriter)
theme:
  name: catppuccin-mocha
  #name: terminal-dark
  override:
    block_quote:
      prefix: "$ "
    footer:
      style: progress_bar
      character: ◉
      # left: "My name is {author}"
      # center: "@myhandle"
      # right: "{current_slide} / {total_slides}"
---

<!-- new_lines: 2 -->
┓ ┏┓   ┏┓     ┳┏┓ \
┃┃┃┣┓┏┓┣┫┏┳┓  ┃┏┛  \
┗┻┛┛┗┗┛┛┗┛┗┗  ┻• 
<!-- new_lines: 1 -->

<!-- column_layout: [1, 1] -->
<!-- column: 1 -->
### Creator of Metis Linux from `github.com/metis-os`

![Metis](./images/metis.gif)

### I make beautiful CLI apps in Rust, C, and more.
### KISS, Unix, and DRY principles.
### Been exploring DevSecOps lately.

<!-- end_slide -->

<!-- new_lines: 2 -->
┏┓ ┓    ┓  ┓    ┏┓ \
┗┓┏┣┓┏┓┏┫┓┏┃┏┓  ┃┃ \
┗┛┗┛┗┗ ┗┻┗┻┗┗   ┗┛

<!-- new_lines: 2 -->
<!-- new_lines: 2 -->

> NOTE: This presentation is made using flakes and neovim on Nix(OS) ❄️ ¹.

<!-- new_lines: 2 -->
<!-- new_lines: 2 -->

#### What is Nix(OS)?
#### A little history.
#### Using Nix on Apple Silicon.
#### Exploring `nix` programming language basics.
#### Using `flakes` and `direnv` to declare development environment.

<!-- end_slide -->

<!-- new_lines: 2 -->
┳┓┳┏┓┏┓ \
┃┃┃ ┃┃  \
┛┗┻┗┛┗┛ (the programming lang)

## `Nix repl` in action
