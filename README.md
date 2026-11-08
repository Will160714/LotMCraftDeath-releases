# LotMCraftDeath-releases

Release jars of LotMCraftDeath, and the **Lord** modpack that uses them.

| | Version |
|---|---|
| Minecraft | **1.21.1** |
| NeoForge | **21.1.265** |
| LOTMCraft | built from the `temp_server` branch; the newest is always the [latest release](https://github.com/Will160714/LotMCraftDeath-releases/releases/latest) |

The pack is managed with [packwiz](https://packwiz.infra.link/). Its URL is:

```
https://raw.githubusercontent.com/Will160714/LotMCraftDeath-releases/main/pack.toml
```

The installer reads this URL each time it runs, downloads any mods that are
missing or out of date, and removes mods that were dropped from the pack.

## Not included

These are in the original Lord instance but are **not** in the pack, because
they aren't published on CurseForge or Modrinth. If you need them, ask whoever
runs the server for the jar and put it in your `mods` folder yourself:

| Mod | Version | File |
|---|---|---|
| NeoOrigins | 2.2.38 | `neoorigins-2_2_38_1_21_1.jar` |
| CommandDisabler | 1.0.3 | `command_disabler-1.0.3.jar` |

Shader packs, mod configs and other personal settings are not included either.

## Playing with Prism Launcher (easiest)

[Prism Launcher](https://prismlauncher.org/) can run the installer
automatically before every launch.

1. Create a new instance: Minecraft **1.21.1**, mod loader **NeoForge
   21.1.265**.
2. Download `packwiz-installer-bootstrap.jar` from
   https://github.com/packwiz/packwiz-installer-bootstrap/releases and put it in
   the instance's `minecraft` folder (right-click the instance → Folder).
3. Edit Instance → Settings → Custom commands → tick it and set
   **Pre-launch command** to:

   ```
   "$INST_JAVA" -jar packwiz-installer-bootstrap.jar https://raw.githubusercontent.com/Will160714/LotMCraftDeath-releases/main/pack.toml
   ```

4. Launch. The first start downloads all the mods; later starts only fetch
   updates.

## Playing with the official Minecraft Launcher

The official launcher can't run the installer for you, so you run it yourself
before playing whenever the pack has changed.

### One-time setup

1. **Install Java 21** if you don't have it (the installers below are Java
   programs): https://adoptium.net/temurin/releases/?version=21 — choose the
   JRE or JDK installer for your system and tick "Add to PATH" if asked.
2. **Install NeoForge 21.1.265.** Download
   [neoforge-21.1.265-installer.jar](https://maven.neoforged.net/releases/net/neoforged/neoforge/21.1.265/neoforge-21.1.265-installer.jar),
   open it, choose **Install client** and click OK. Close the Minecraft
   Launcher first.
3. **Make a folder for the pack**, separate from your normal game, e.g.
   `C:\Games\Lord` (Windows) or `~/Games/Lord` (macOS/Linux).
4. **Put the installer in that folder.** Download
   `packwiz-installer-bootstrap.jar` from
   https://github.com/packwiz/packwiz-installer-bootstrap/releases into it.
5. **Create an update script in the same folder.**

   *Windows:* create `update.bat` (in Notepad, "Save as type: All files")
   containing:

   ```bat
   @echo off
   cd /d "%~dp0"
   java -jar packwiz-installer-bootstrap.jar https://raw.githubusercontent.com/Will160714/LotMCraftDeath-releases/main/pack.toml
   pause
   ```

   *macOS/Linux:* create `update.sh` containing the lines below, then run
   `chmod +x update.sh` once:

   ```sh
   #!/bin/sh
   cd "$(dirname "$0")"
   java -jar packwiz-installer-bootstrap.jar https://raw.githubusercontent.com/Will160714/LotMCraftDeath-releases/main/pack.toml
   ```

6. **Run the script** (double-click `update.bat`, or `./update.sh`). A window
   shows the download progress; when it finishes, the folder has a `mods`
   folder with the pack's mods.
7. **Add an installation in the Minecraft Launcher.** Installations → New
   installation:
   - **Version:** `release neoforge-21.1.265` (type "neoforge" to find it)
   - **Game directory:** the folder from step 3
   - **More options → JVM arguments:** change `-Xmx2G` to at least `-Xmx6G`
     (the pack is large; use `-Xmx8G` if you have 16 GB of RAM or more)

### Every time you play

Run `update.bat` / `update.sh` first, then start the installation from the
Minecraft Launcher. If the pack hasn't changed, the script finishes in a few
seconds.

## Server

Put `packwiz-installer-bootstrap.jar` in the server folder and run this before
starting the server (it only installs the mods a server needs):

```
java -jar packwiz-installer-bootstrap.jar -g -s server https://raw.githubusercontent.com/Will160714/LotMCraftDeath-releases/main/pack.toml
```

## Editing the pack

Mod entries are in `mods/*.pw.toml`. After changing anything, run
`packwiz refresh` and commit `index.toml` and `pack.toml` with your change.
`mods/lotmcraft.pw.toml` is updated automatically after each LOTMCraft release.
