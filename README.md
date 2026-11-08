# LotMCraftDeath-releases

Release jars of LotMCraftDeath, and a packwiz pack that installs and keeps
the **LOTMCraft** mod up to date. The pack contains only LOTMCraft; its
libraries (TerraBlender, LDLib2, Photon, PlayerAnimationLib) are bundled
inside the jar, so nothing else is needed to run it.

| | Version |
|---|---|
| Minecraft | **1.21.1** |
| NeoForge | **21.1.265** |
| LOTMCraft | built from the `temp_server` branch; the newest is always the [latest release](https://github.com/Will160714/LotMCraftDeath-releases/releases/latest) |

The pack is managed with [packwiz](https://packwiz.infra.link/). Its URL is:

```
https://raw.githubusercontent.com/Will160714/LotMCraftDeath-releases/main/pack.toml
```

The installer reads this URL each time it runs and downloads the newest
LOTMCraft jar if yours is missing or out of date.

## Other mods

No other mods are included. If the server you play on uses more mods, add
them to the same `mods` folder yourself (or with your launcher). The installer
only manages the LOTMCraft jar and leaves other mods in the folder alone.

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

4. Launch. The first start downloads LOTMCraft; later starts only fetch
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
   folder containing the LOTMCraft jar.
7. **Add an installation in the Minecraft Launcher.** Installations → New
   installation:
   - **Version:** `release neoforge-21.1.265` (type "neoforge" to find it)
   - **Game directory:** the folder from step 3
   - **More options → JVM arguments:** change `-Xmx2G` to at least `-Xmx4G`
     (more if you add other large mods)

### Every time you play

Run `update.bat` / `update.sh` first, then start the installation from the
Minecraft Launcher. If LOTMCraft hasn't changed, the script finishes in a few
seconds.

## Playing with the CurseForge app

The CurseForge app can't run the installer before launch, but because the pack
is a single mod there are two easy ways to use it.

### One-time setup

1. In the CurseForge app, go to Minecraft → **Create Custom Profile**.
2. Choose Minecraft **1.21.1**, mod loader **NeoForge**, and version
   **21.1.265** (any 21.1.217 or newer works). Create it.
3. Open the profile, click the **⋯** menu → **Open Folder**. This opens the
   profile's folder (normally
   `C:\Users\<you>\curseforge\minecraft\Instances\<profile name>`).
4. Optional but recommended: profile **⋯** → **Profile Options** → turn off
   "Use System Memory Settings" and allocate at least 4 GB.

Then pick **one** of the options below.

### Option A: add the jar by hand (simplest)

1. Download the `lotmcraft-….jar` file from the
   [latest release](https://github.com/Will160714/LotMCraftDeath-releases/releases/latest).
2. Put it in the `mods` folder inside the profile's folder.
3. Play from the CurseForge app.

When a new release comes out, delete the old `lotmcraft-….jar` from `mods`
and download the new one. Never keep two LOTMCraft jars in `mods` at once.

### Option B: update automatically with a script

1. Install Java 21 if you don't have it:
   https://adoptium.net/temurin/releases/?version=21 (tick "Add to PATH" if
   asked).
2. Download `packwiz-installer-bootstrap.jar` from
   https://github.com/packwiz/packwiz-installer-bootstrap/releases into the
   profile's folder.
3. Create `update.bat` in the profile's folder with the same contents as in
   the official launcher section above.
4. Double-click `update.bat` before you play. It downloads the newest
   LOTMCraft jar into `mods` and removes the old one.
5. Play from the CurseForge app. CurseForge lists LOTMCraft as a mod you added
   yourself; that's expected.

Don't mix the options: if you use the script, let it manage the LOTMCraft jar
and don't add or remove it by hand.

## Server

Put `packwiz-installer-bootstrap.jar` in the server folder and run this before
starting the server:

```
java -jar packwiz-installer-bootstrap.jar -g -s server https://raw.githubusercontent.com/Will160714/LotMCraftDeath-releases/main/pack.toml
```

## Editing the pack

`mods/lotmcraft.pw.toml` is updated automatically after each LOTMCraft
release. If you edit the pack by hand, run `packwiz refresh` and commit
`index.toml` and `pack.toml` with your change.
