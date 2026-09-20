# RevolunixOS system modules

Reusable NixOS and Home Manager configuration fragments for RevolunixOS. The
flake exposes separate CLI and graphical bases as importable paths.

## Exported attributes

| Attribute | Contents |
| --- | --- |
| `configsImports.base.cli.system` | Boot, services, programs, and console configuration |
| `configsImports.base.cli.home` | CLI user programs and writable configuration helpers |
| `configsImports.base.graphical.system` | Graphical boot, services, programs, and polkit settings |
| `configsImports.base.graphical.home` | Hyprland, Waybar, Rofi, Kitty, GTK, tmux, lock screen, and related user configuration |

## Flake input

```nix
inputs.revolunix-system = {
  url = "github:RevolunixOS/module-system";
  inputs.nixpkgs.follows = "nixpkgs";
};
```

The exported paths can then be imported from a consuming flake, for example:

```nix
imports = [
  inputs.revolunix-system.configsImports.base.cli.system
];
```

Home Manager fragments belong in a Home Manager module, while `system`
fragments belong in a NixOS module.

> [!WARNING]
> The current `flake.nix` destructures a `home-manager` input without declaring
> it. Fix or remove that parameter before relying on direct flake evaluation.
> The repository also contains personal application state and should be audited
> before reuse.

## Development

```bash
nix flake show
nix fmt
```

The flake pins `nixos-24.05`; update and test the input before targeting a newer
NixOS release.

## License

See [`LICENSE`](LICENSE).
