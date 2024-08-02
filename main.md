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

┏┓ ┓    ┓  ┓    ┏┓ \
┗┓┏┣┓┏┓┏┫┓┏┃┏┓  ┃┃ \
┗┛┗┛┗┗ ┗┻┗┻┗┗   ┗┛

<!-- new_lines: 2 -->
<!-- new_lines: 2 -->

> NOTE: This presentation is made using flakes and neovim on Nix(OS) ❄️ ¹.

## The source is availble at: `github:pwnwriter/PTN11`

<!-- new_lines: 2 -->
<!-- new_lines: 2 -->

### What is Nix(OS)?
### A little history.
### `Nix` in action.
### `Nix` programming language basics.
### Using `flakes` and `direnv` to declare development environment.
### `home-manager` and `nix-darwin` in showcase.

<!-- end_slide -->


┳┓•    ┏  ┏┓┏┓  ┓  \
┃┃┓┓┏  ┃  ┃┃┗┓  ┃  \
┛┗┗┛┗  ┗  ┗┛┗┛  ┛  

<!-- new_lines: 2 -->

### Nix :

 - Package manager
 - A functional programming language
 - An entire linux distro based around nix, nixpkgs

### Nixpkgs : 

- Just a repo on github `github:nixos/nixpkgs` containing the largest most upto
date derivations of packages to install via `nix`.

<!-- new_lines: 2 -->

### Pros of using Nix:


| **Aspect**      | **Description**                                             |
|-----------------|-------------------------------------------------------------|
| **Declarative** | Configuration is defined through clear, descriptive specifications rather than step-by-step scripts. |
|                 |                                                             |
|                 | - [x] `$ apt install git`                                  |
|                 |                                                             |
|                 | ```nix                                                      |
|                 | {                                                           |
|                 |   environment.systemPackages = with pkgs; [  nginx ];         |
|                 | }                                                           |
|                 | ```                                                       |
| **Immutable**   | Ensures stability by preventing unintended modifications. |
|                 |                                                             |
|                 | - Changes require explicit updates.                        |
|                 |                                                             |
| **Reproducible** | Guarantees that the same environment can be recreated reliably. |
|                 |                                                             |
|                 | - Identical software configurations across multiple machines. |
|                 | - Example `upnull` script                                       |

<!-- end_slide -->

┏┓┓         •     \
┗┓┣┓┏┓┓┏┏  ╋┓┏┳┓┏┓ \
┗┛┛┗┗┛┗┻┛  ┗┗┛┗┗┗ (Installing nix)
<!-- new_lines: 2 -->

## Nix can be installed via different ways: 

1. As an Operating system
2. As a package manager on *nix os

###### Install `nix` using **determinates-systems nix installer**.

  - `curl --proto '=https' --tlsv1.2 -sSf -L https://install.determinate.systems/nix | sh -s -- install`

##### why?

*. Installs Nix with `flake` support and the unified CLI features

*. Easy to uninstall (You'll never do that yes? yes? yes!!)

*. Written in `rust` Btw!!

<!-- end_slide -->

┳┓┳┏┓┏┓ \
┃┃┃ ┃┃  \
┛┗┻┗┛┗┛ (The programming lang)

Nix REPL is similar to a Python shell or a Bash shell, but for Nix. For more do `:?`.

# `Nix repl` in action

### Evaluating Expressions

```bash
nix-repl> 2 + 3
5
```
### Defining Variables

```bash
nix-repl> let x = 10 in x * 2
20
```
### Inspecting Package Metadata

```bash
$ nix repl
nix-repl> :l <nixpkgs>
Added 22251 variables.

nix-repl> (import <nixpkgs> {}).haylxon
«derivation /nix/store/m7g6612yf7flkrrllp6rjhavxbn68sih-haylxon-1.0.0.drv»

nix-repl> (import <nixpkgs> {}).haylxon.meta.description
"Save screenshots of urls and webpages from terminal"
```
<!-- end_slide -->

┏┓┓  ┓     \
┣ ┃┏┓┃┏┏┓┏ \
┻ ┗┗┻┛┗┗ ┛  

### What the heck is a flake? 
A `flake.nix` file is an attribute set with two attributes called inputs and outputs.

- Inputs : Specify dependencies, like other flakes or repositories.
```nix
{
    inputs = {
        nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable";
    };
}
```
- Outputs : Define what the flake provides, such as packages or configurations.

```nix
{
    outputs = { self, nixpkgs }: {
        packages.x86_64-linux.myPackage = foo bar buzz;
    };
}
```

Flakes are experimental and disabled by default. Enable them `/etc/nix/nix.conf` or `~/.config/nix/nix.conf`

```bash
experimental-features = nix-command flakes
```
<!-- end_slide -->

### Why flakes?

#### Using `nix-shell -p git` or a `shell.nix` file like:

```nix
{ pkgs ? import <nixpkgs> {} }:

pkgs.mkShell {
  buildInputs = [ pkgs.git ];
}
```

Installs `git` but relies on the system's current Nixpkgs channel. This means
your environment is dependent on the versions and state of the system's
channel.Flakes provide a more consistent and reproducible environment by specifying
exact dependencies and versions, independent of the system’s channel.

## Writing a `flake.nix` to install really an old version of `git`: independent of system version


┳┓•  ┏┓    \
┃┃┓┏┓┣ ┏┓┓┏ \
┻┛┗┛ ┗┛┛┗┗┛ (direnv setup)

`Direnv` allow us to simply oad and unload environment variables depending on the
current directory, while `nix-direnv` is an add-on to load and unload `flake.nix` environment.

Current presentation directory is an example of this.

<!-- end_slide -->

┓┏         ┳┳┓            \
┣┫┏┓┏┳┓┏┓━━┃┃┃┏┓┏┓┏┓┏┓┏┓┏┓ \
┛┗┗┛┛┗┗┗   ┛ ┗┗┻┛┗┗┻┗┫┗ ┛  \
                     ┛ (github:nix-community/home-manager)

### Home Manager: A tool for managing user-specific configurations and dotfiles using Nix, allowing for declarative setup of personal environments.

Building a starship prompt based on the host.

```nix
{ lib, pkgs, ... }:

let
  macos_prompt = {"  "};

  linux_prompt = {"  " };
in
{
  programs.starship = {
    enable = true;
    settings = {
      format = lib.concatStrings [
        "$character"
      ];
      character = if pkgs.stdenv.isDarwin then macos_prompt else linux_prompt;
    };
  };
}
```

#### Installing packages:

```nix
{
home.packages = with pkgs [ git ];
}
```

<!-- end_slide -->

┳┓•     ┓       •   \
┃┃┓┓┏  ┏┫┏┓┏┓┓┏┏┓┏┓ \
┛┗┗┛┗  ┗┻┗┻┛ ┗┻┛┗┛┗ (github:LnL7/nix-darwin)

### `nix-darwin` is a module for darwin(macos) systems to bring the convenience of a declarative system approach to macOS.


Nix-darwin example package install

```nix
{
environment.systemPackages = with pkgs; [kubectl];
}
```
