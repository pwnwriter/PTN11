#### Presentation for [Pentester Nepal's][ptn] 11th anniversary: Using Nix on Apple Silicon and declarative development environments.

#### Notes: 
- Install `nix` using [__`determinates-systems nix installer`__][determinate],

  - `curl --proto '=https' --tlsv1.2 -sSf -L https://install.determinate.systems/nix | sh -s -- install`

- Dev shell of [`presenterm`][presenterm] 

  - If you have `nix-direnv`
    - Run: `$ direnv allow`
    - Else :  `$ nix develop` to enter a shell with all deps installed.
  
  - Run `$ presenterm main.md` to show presentation in your terminal.

All contents here are licensed under the [MIT License](Mit).

[determinate]: https://determinate.systems
[ptn]: https://pentesternepal.com
[presenterm]: https://github.com/mfontanini/presenterm
[Mit]: ./License

