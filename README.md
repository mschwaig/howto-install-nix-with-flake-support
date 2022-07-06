How to set up the Nix package manager with flake support
===

These steps help you set up the Nix package manager with support for a experimental more user-friendly command language and a defined package format called flakes that makes it easier to create builds in a strictly determined environment, so that they create the same outputs on various machines or in CI.

## Step 1: Install the Nix package manager

To install Nix, please follow the instructions at [https://nixos.org/download.html](https://nixos.org/download.html), since they are quite good.

If you want to know more before installing you can [read the install section in the Nix manual directly](https://nixos.org/manual/nix/stable/#ch-installing-binary).

You might have to re-open your terminals, restart your graphical session or even reboot after this step.

## Step 2: Enable the right experimental features

Recent releases of Nix already ship with the required code for flakes, but leave them behind a feature flag that you have to enable.

To enable them, you have to add the following lines to `/etc/nix/nix.conf`

```
experimental-features = nix-command flakes
```

and on a multi-user install (invoked with --daemon) restart the nix daemon so it can pick up the newly set experimental options.
```
systemctl restart nix-daemon.service
```

## Step 3: Verify Nix Install

The following command should now give similar output.

```
$ nix flake --help
```

```
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

