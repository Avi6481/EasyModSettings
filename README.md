# Easy Mod Settings

Easy Mod Settings adds a Mod Settings button to the pause menu. It opens the game's own Settings screen with your mods in it, using the game's own toggles, sliders, lists and buttons.

Works on console.

Mods using it:

- [Easy First Equip](https://github.com/Avi6481/EasyFirstEquip)
- EasyTrainer Lite

## Usage

Pause Menu > Mod Settings. Pick a mod on the left (or 9 / 0) and its pages are the tabs up top. Defaults (F1) resets the page and Esc closes it. Controller should work too, I just haven't fully tested it yet.

## Adding your mod

On console every mod is cooked on its own, so your mod can't call Mod Settings directly. Instead each mod adds a link to a chain in a vanilla blackboard slot (`UIGameData.UIjailbreakData`) and Mod Settings sends its messages down that chain. If Mod Settings isn't installed, your mod just uses its defaults.

1. Copy `Template/MyModSettings.script` into your mod.
2. Replace `MyMod` with your mod's name and `mymod` with a short lowercase prefix.
3. Put your options in `Spec()` and update `Default()`, `IsToggle()`, `IsChoice()` and `Ids()` to match.
4. Read an option with `MyModSettings.Get(game, "mymod.something")`, using the game from the player (`player.GetGame()`).

Load a save and your mod shows up in the list. [Easy First Equip](https://github.com/Avi6481/EasyFirstEquip) is a full example.

### Spec lines

One option per line. Fields are split by `|`, `-` means empty and choices are split by `;`.

    mod|<modId>|<name>|<version>|<author>|<description>
    page|<pageKey>|<title>
    header|<label>
    toggle|<id>|<label>|<tip>|<default 0/1>|<dependsOn>
    slider|<id>|<label>|<tip>|<min>|<max>|<step>|<default>|<decimals>|<unit>|<dependsOn>
    choice|<id>|<label>|<tip>|<A;B;C>|<default index>|<dependsOn>
    button|<id>|<label>|<tip>|<button text>|<dependsOn>
    confirm|<id>|<label>|<tip>|<dependsOn>
    reset|<id>|<label>|<tip>
    submenu|<pageKey>|<label>|<tip>|<dependsOn>
    info|<id>|<label>|<tip>
    note|<text>

`page` starts a new tab. `dependsOn` is a toggle id, and the row greys out while that toggle is off. `reset` and `confirm` need two presses.
