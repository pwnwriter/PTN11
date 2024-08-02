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

<!-- column_layout: [1, 2] -->
<!-- column: 0 -->
### Creator of Metis Linux from `github.com/metis-os`

### I make beautiful CLI apps in Rust, C, and more.
### KISS, Unix, and DRY principles.
### Been exploring DevSecOps lately.


<!-- column: 1 -->
![Metis](./media/metis.gif)

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

### What is Nix(OS)?
### A little history.
### `Nix` programming language basics.
### `Nix` in action.
### `home-manager` and `nix-darwin` in showcase.
### Using `flakes` and `direnv` to declare development environment.

<!-- end_slide -->

<!-- new_lines: 2 -->

┳┓•    ┏  ┏┓┏┓  ┓  \
┃┃┓┓┏  ┃  ┃┃┗┓  ┃  \
┛┗┗┛┗  ┗  ┗┛┗┛  ┛  

<!-- new_lines: 2 -->

### Nix :

 - Package manager
 - A functional programming language
 - An entire linux distro based around nix, nixpkgs

### Nixpkgs : 

- Just a repo on github `github:nixos/nixpkgs` containing the derivations of packages to install via `nix`.
<!-- new_lines: 2 -->

### Pros of using Nix:


| **Aspect**      | **Description**                             |
|-----------------|---------------------------------------------|
| **Declarative** | System config is defined, not scripted.    |
|                 |                                            |
|                 | - [x] `$ apt install git`                  |
|                 |                                            |
| **Immutable**   | Prevents unintentional changes.             |
|                 |                                            |
|                 | - Changes require explicit updates.     |
|                 |                                            |
| **Reproducible**| The same setup can be reproduced later.            |

<!-- end_slide -->

<!-- new_lines: 3 -->

<!-- end_slide -->

<!-- new_lines: 4 -->
┳┓┳┏┓┏┓ \
┃┃┃ ┃┃  \
┛┗┻┗┛┗┛ (The programming lang)

## `Nix repl` in action
