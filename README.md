# LotMCraftDeath-releases

Release jars of LotMCraftDeath, and the **Lord** packwiz modpack that uses them
(Minecraft 1.21.1, NeoForge 21.1.265).

Pack URL:

```
https://raw.githubusercontent.com/Will160714/LotMCraftDeath-releases/main/pack.toml
```

## Players (Prism Launcher)

1. Create a Minecraft 1.21.1 instance with NeoForge 21.1.265.
2. Download `packwiz-installer-bootstrap.jar` from
   https://github.com/packwiz/packwiz-installer-bootstrap/releases and put it in
   the instance's `.minecraft` folder.
3. Edit Instance → Settings → Custom commands → Pre-launch command:

   ```
   "$INST_JAVA" -jar packwiz-installer-bootstrap.jar https://raw.githubusercontent.com/Will160714/LotMCraftDeath-releases/main/pack.toml
   ```

Mods are installed and updated every time the game starts.

## Server

Put `packwiz-installer-bootstrap.jar` in the server folder and run this before
starting the server:

```
java -jar packwiz-installer-bootstrap.jar -g -s server https://raw.githubusercontent.com/Will160714/LotMCraftDeath-releases/main/pack.toml
```

## Editing the pack

Mod entries are in `mods/*.pw.toml`. After changing anything, run
`packwiz refresh` and commit `index.toml` and `pack.toml` with your change.
