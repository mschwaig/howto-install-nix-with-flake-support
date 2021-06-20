How to set up the Nix package manager with flake support
===

These steps help you set up the Nix package manager with support for a experimental more user-friendly command language and a defined package format called flakes that makes it easier to create builds in a strictly determined environment, so that they create the same outputs on various machines or in CI.

## Step 1: Install the Nix package manager

Run the following command with sudo but not directly as root:

```
$ curl -L https://nixos.org/nix/install | sh
```

See https://nixos.org/download.html for more info.
Note that you can split up the abovementioned commands in accordance with your own risk-appetite.

## Step 2: Enable the right experimental features

First run the following comand
```
nix-env -iA nixpkgs.nixFlakes
```

and then add the following lines to `~/.config/nix/nix.conf`

```
experimental-features = nix-command flakes ca-references
```

## Step 3: Verify

The following command should now give similar output.

```
$ nix flake --help
Usage: nix flake COMMAND FLAGS... ARGS...

Common flags:

Available commands:
  archive      copy a flake and all its inputs to a store
  check        check whether the flake evaluates and run its tests
  clone        clone flake repository
  info         list info about a given flake
  init         create a flake in the current directory from a template
  list-inputs  list flake inputs
  new          create a flake in the specified directory from a template
  show         show the outputs provided by a flake
  update       update flake lock file

Note: this program is EXPERIMENTAL and subject to change.
```

## Step 4: Install something
```
nix profile install github:idris-lang/Idris2 
```
