# ublueBG

[![build-ublue](https://github.com/bgibryan/ublueBG/actions/workflows/build.yml/badge.svg)](https://github.com/bgibryan/ublueBG/actions/workflows/build.yml)

These are custom images created from the uBlue starting point template. Minor changes have been implemented to pre installed and omitted packages as well as providing builds for both intel/amd and nvidia for Gnome and KDE Plasma desktop environments.

For more info, check out the [uBlue homepage](https://universal-blue.org/) and the [main uBlue repo](https://github.com/ublue-os/main/)

## Make Your Own Template!

See the [Make Your Own -page in the documentation](https://universal-blue.org/tinker/make-your-own/) for quick setup instructions for setting up your own repository based on this template.

Don't worry, it only requires some basic knowledge about using the terminal and git.

### [yafti](https://github.com/ublue-os/yafti/)

`yafti` is the uBlue "first boot" installer. It shows up the first time a user logs into uBlue. By default, the menu also shows up again anytime the image's yafti configuration differs from the user's last encounter, so feel free to expand or modify your custom image's yafti configuration over time. Your users will then see the yafti menu again after the OS update, and will be given a chance to install any new additions.

Its configuration can be found in `/usr/share/ublue-os/firstboot/yafti.yml` of the installed OS. It includes an optional selection of Flatpaks to install, along with a new group that's automatically added for all Flatpaks declared in `recipe.yml`. You can look at what's done in the `yafti.yml` config and modify it to your liking (in the repository, before building the image, since the installed system file is immutable).

If you want to completely disable yafti, simply set the recipe's `firstboot.yafti` flag to `false`, which then removes all yafti-related files and configurations from your final image. The files in `usr/share/ublue-os/firstboot/` are responsible for automatically running yafti at login, and they will *only* be bundled in your image if `yafti` is enabled in your recipe!

## Just

The `just` task runner is included in `ublue-os/main`-derived images, and we have provided several template commands which help you perform further customization after first boot.

You can merge our template justfiles into your own local configuration. When `just` supports [include directives](https://just.systems/man/en/chapter_52.html), you will instead be able to simply include these paths into your own justfile, without having to copy anything manually.

Run the following commands when you're logged into the operating system, to merge uBlue's provided configurations into your own user config. (The "touch" command is only necessary on certain shells which won't let you merge into non-existent files.)

```sh
touch ~/.justfile
cat /usr/share/ublue-os/just/main.just >> ~/.justfile
cat /usr/share/ublue-os/just/custom.just >> ~/.justfile
```

After doing that, you'll be able to run the following commands:

- `just` - Show all tasks, more will be added in the future
- `just bios` - Reboot into the system bios (Useful for dualbooting)
- `just changelogs` - Show the changelogs of the pending update
- Set up distroboxes for the following images:
  - `just distrobox-boxkit`
  - `just distrobox-debian`
  - `just distrobox-opensuse`
  - `just distrobox-ubuntu`
- `just setup-flatpaks` - Install all of the flatpaks declared in recipe.yml
- `just setup-gaming` - Install Steam, Heroic Game Launcher, OBS Studio, Discord, Boatswain, Bottles, and ProtonUp-Qt. MangoHud is installed and enabled by default, hit right Shift-F12 to toggle
- `just nix-me-up` - Install Nix with dnkmmr69420's Nix Silverblue install script
- `just update` - Update rpm-ostree, flatpaks, and distroboxes in one command

Check the [just website](https://just.systems) for tips on modifying and adding your own recipes.

