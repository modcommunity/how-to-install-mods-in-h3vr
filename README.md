A guide on how to **download** and **install mods** in [Hot Dogs, Horseshoes & Hand Grenades](https://store.steampowered.com/app/450540/Hot_Dogs_Horseshoes__Hand_Grenades/) (H3VR) on PC.

H3VR is a VR-only sandbox shooter with one of the longest running mod scenes in VR, and practically all of it lives on [Thunderstore](https://thunderstore.io/c/h3vr/). Mods are [BepInEx](https://github.com/BepInEx/BepInEx) plugins, and the gun mods everybody comes for sit on top of a small stack of shared libraries.

Our example is [Meats ModulAR](https://thunderstore.io/c/h3vr/p/Meat_banono/Meats_ModulAR/), a large modular AR pack. It is deliberately not a simple mod, because H3VR gun packs rarely are and the dependency chain is the thing worth understanding.

[**View Guide On TMC (Recommended Due To Better Formatting)**](https://moddingcommunity.com/blog/how-to-install-mods-in-h3vr/)

## Table Of Contents
* [Requirements](#requirements)
* [VR Only, No Flat Mode](#vr-only-no-flat-mode)
* [What Gets Installed](#what-gets-installed)
    * [BepInEx](#bepinex)
    * [OtherLoader And Friends](#otherloader-and-friends)
* [Installing With r2modman](#installing-with-r2modman)
* [Installing With Thunderstore Mod Manager](#installing-with-thunderstore-mod-manager)
* [Installing Manually](#installing-manually)
* [Installing With The TMC App](#installing-with-the-tmc-app)
* [Finding Modded Guns In-Game](#finding-modded-guns-in-game)
* [Managing Mods Over Time](#managing-mods-over-time)
* [Troubleshooting](#troubleshooting)
* [Conclusion](#conclusion)
* [See Also](#see-also)

## Requirements
* A PC running **Windows 10** or later. Linux via Proton works, with an extra launch option covered below.
* **H3VR** on Steam.
* A working VR headset and runtime. H3VR supports SteamVR headsets along with Oculus and Windows Mixed Reality devices through it.
* **Several GB** of free space. Gun packs carry a lot of models, textures and audio, and a serious H3VR mod list gets large quickly.
* [7-Zip](https://www.7-zip.org/) or equivalent if you install by hand.

H3VR is single player with no anti-cheat, so there is nothing to worry about on that front.

## VR Only, No Flat Mode
Worth saying plainly before anything else. H3VR is a VR exclusive with no flatscreen mode, and mods do not change that. If you do not have a headset, none of this applies.

There are no console versions either, so everything below is PC only.

## What Gets Installed
### BepInEx
[BepInExPack H3VR](https://thunderstore.io/c/h3vr/p/BepInEx/BepInExPack_H3VR/) is the loader. It goes into the game folder, hooks the game at launch, and loads plugins from `BepInEx/plugins`.

Use the H3VR-specific pack rather than generic BepInEx. It is pinned at 5.4.1700 and preconfigured for this game, and the community builds against it.

### OtherLoader And Friends
This is where H3VR differs from most BepInEx games. A gun pack is not really "code", it is a bundle of items, and getting those items into H3VR's spawner and its progression systems needs shared infrastructure.

Meats ModulAR depends on a handful of these:

| Dependency | What it does |
| ---------- | ------------ |
| [OtherLoader](https://thunderstore.io/c/h3vr/p/devyndamonster/OtherLoader/) | Loads custom item bundles into the game and handles the spawner entries for them. |
| [H3VRUtilities](https://thunderstore.io/c/h3vr/p/WFIOST/H3VRUtilities/) | A long-standing shared library that a huge amount of the scene builds on. |
| [OpenScripts](https://thunderstore.io/c/h3vr/p/cityrobo/OpenScripts/) | Generic behaviour scripts mod authors attach to custom parts. |
| [FTW Arms AFCL](https://thunderstore.io/c/h3vr/p/Andrew_FTW/FTW_Arms_AFCL/) | A shared attachment and parts library for modular weapon mods. |
| Meats ModulARpt2 | The mod's own second half, split because of Thunderstore package size limits. |

Every one of these has to be present, at a compatible version, before the gun pack does anything. That is the entire argument for using a mod manager here rather than downloading files by hand.

**NOTE** - Large packs getting split into part 1 and part 2 packages is normal on H3VR Thunderstore. If you install the first half only, expect missing guns rather than a clean error.

## Installing With r2modman
[r2modman](https://thunderstore.io/c/h3vr/p/ebkr/r2modman/) is the usual recommendation for H3VR and the one most mod pages assume.

1. Download r2modman from [Thunderstore](https://thunderstore.io/c/h3vr/p/ebkr/r2modman/) or from [GitHub releases](https://github.com/ebkr/r2modmanPlus/releases).
2. Launch it and pick **H3VR**.
3. Create a profile. Given how big H3VR mod lists get, having one profile per loadout theme is genuinely useful rather than just tidy.
4. Click **Online**, search for **Meats ModulAR**, and open the result by **Meat_banono**.
5. Click **Download**, then **Download with dependencies**.
6. Wait. This pulls several hundred MB and includes OtherLoader, H3VRUtilities, OpenScripts, the FTW parts library and ModulAR part 2.
7. Check the **Installed** tab. Everything should be listed with no warning icons.
8. Click **Start modded**.

Launching H3VR from Steam instead starts it vanilla. The mods are attached by the manager at launch time, so the launch has to come from r2modman.

## Installing With Thunderstore Mod Manager
[Thunderstore Mod Manager](https://www.overwolf.com/app/Thunderstore-Thunderstore_Mod_Manager) is built on r2modman and works the same way behind an Overwolf wrapper.

1. Install it and choose **H3VR**.
2. Pick a profile.
3. Click **Get mods**, find **Meats ModulAR**, and click **Download**.
4. Accept the dependency list.
5. Click **Start modded**.

Either manager is fine. r2modman is the better pick on Linux, and the only one with a macOS build, though H3VR itself has no macOS release.

## Installing Manually
Possible, and a real chore for a mod like this one. Doing it once for a small mod is educational; doing it for a full gun pack is not a good use of an evening.

Find your game folder by right-clicking **H3VR** in Steam, then **Manage** and **Browse local files**:

```
C:\Program Files (x86)\Steam\steamapps\common\H3VR
```

1. Download [BepInExPack H3VR](https://thunderstore.io/c/h3vr/p/BepInEx/BepInExPack_H3VR/) with **Manual Download** and extract it.
2. Copy the **contents** of the `BepInExPack_H3VR` folder into the H3VR folder, so `BepInEx`, `doorstop_config.ini` and `winhttp.dll` sit beside `h3vr.exe`.
3. Launch the game once and quit, which creates `BepInEx/plugins`.
4. Download every dependency listed on the mod's Thunderstore page, at the exact versions it names, plus anything those depend on in turn.
5. Extract each and copy its contents into `BepInEx/plugins`, keeping each mod in its own subfolder so you can tell them apart later.
6. Do the same for Meats ModulAR and ModulAR part 2.

**WARNING** - Keep each mod in its own folder under `plugins`. H3VR mods ship asset bundles with generic names, and flattening several packs into one folder is a reliable way to have them overwrite each other.

**TIP** - OtherLoader reads item bundles from the plugin folders it scans. If a gun pack installs cleanly but no new guns appear in the spawner, a mangled folder layout from a manual install is the first thing to check.

## Installing With The TMC App
One more, and it is ours. [The TMC App](https://moddingcommunity.com/tmc-app) is a mod manager and server browser we build. Its **sandboxes** are named mod profiles per game, each with its own load order and deployment method, and switching between them re-downloads nothing. For a game where people keep separate lists for separate loadouts and where every list takes an age to load, that is a feature with obvious appeal.

**H3VR is not in its supported games list yet.** Adding a game means four JSON files rather than code, so it is not a big piece of work.

Before you get your hopes up: **the app is in very early development.** Its README says as much and so will we. Much of it is only partially tested, and for a mod stack as dependency-heavy as H3VR's, r2modman is still the tool to rely on. Try the app next to it by all means, and if you do, tell us how it went. Early feedback is worth more to us than almost anything else at this point.

It is **open source** under GPL-3.0 at [github.com/modcommunity/tmc-app](https://github.com/modcommunity/tmc-app). [The issue tracker](https://github.com/modcommunity/tmc-app/issues) takes bugs and feature requests, pull requests are welcome, and the repository documents how a game gets added if you want to contribute H3VR support.

Installing it:

* **Linux**: one line, no root and no package manager.

```bash
curl -fsSL https://raw.githubusercontent.com/modcommunity/tmc-app/main/scripts/install.sh | sh
```

* **Windows**: the `setup.exe` or `setup.msi` from the [releases page](https://github.com/modcommunity/tmc-app/releases). There is a portable build too, though it does not register the launcher entry or the `tmc://` link handler.
* **macOS**: the `.dmg` from the same releases page.

## Finding Modded Guns In-Game
Installed weapon mods do not replace anything. They appear alongside the vanilla arsenal.

Load into any sandbox scene and open the **Item Spawner**. Modded guns show up in the same category lists as the stock ones, usually with the mod's own tags or a separate page depending on how the author set it up. Meats ModulAR adds modular AR receivers plus a large set of parts, so expect entries in both the firearm and the attachment categories.

If the game boots with mods loaded but the spawner looks stock, that is an OtherLoader problem rather than a BepInEx problem, and the BepInEx console will usually say so.

## Managing Mods Over Time
r2modman shows an update badge next to anything with a newer Thunderstore release, and **Update all** takes care of the list. Because H3VR gun packs depend on shared libraries, updating one mod can pull a newer library that an older pack was not built against. Cloning a profile before a big update round is the cheap insurance here.

Disabling a mod in the installed list leaves its files alone. Uninstalling removes them.

To return to vanilla entirely, delete `BepInEx`, `doorstop_config.ini` and `winhttp.dll` from the game folder. Steam's file verification will not remove them, because Steam did not install them.

## Troubleshooting
**Game launches with no mods.** You started it from Steam. Use **Start modded**.

**No BepInEx console.** BepInEx is not loading. Check that `winhttp.dll` is directly next to `h3vr.exe`.

**Mods load but no new guns in the spawner.** OtherLoader is missing, out of date, or the item bundles are in the wrong place. Reinstall the mod with dependencies through your manager.

**Long load times and stutter.** Normal past a certain mod count. H3VR loads every item bundle at startup, and big lists genuinely do take a while. Splitting mods across profiles rather than running everything at once helps a lot.

**Missing textures or pink models.** Usually a half-installed pack, most often a part 2 package that was skipped.

**Crash on startup after a game update.** H3VR updates in fairly large chunks and mods break with them. Move `BepInEx/plugins` aside to confirm, then wait for the authors.

**Linux and Proton.** Set H3VR's Steam launch options to `WINEDLLOVERRIDES="winhttp=n,b" %command%`. r2modman handles this itself when you launch through it.

## Conclusion
H3VR mod installs are straightforward as long as you let a mod manager resolve the dependency chain. Install r2modman, pick H3VR, download with dependencies, and launch modded.

The two H3VR-specific things worth carrying with you: gun packs need OtherLoader and its friends to show up in the spawner at all, and big packs get split into multiple Thunderstore packages that all need installing.

If you have time to spare, the [TMC App](https://github.com/modcommunity/tmc-app) is open source, early in development, and feedback on it would be genuinely appreciated.

## See Also
* [H3VR on Thunderstore](https://thunderstore.io/c/h3vr/)
* [H3VR Modding Wiki](https://h3vr-modding.github.io/wiki/) - The current community modding wiki.
* [H3VR Modding Discord](https://discord.gg/Hggg7wh)
* [Official H3VR Wiki](https://wiki.h3vr.com/) - The game wiki rather than a modding one, but useful for working out what is vanilla.
* [TMC App](https://github.com/modcommunity/tmc-app)

We keep this guide current as best we can, but H3VR, BepInEx and the shared libraries all move independently. If an instruction here no longer matches what you are seeing, please report it or open a [pull request](https://github.com/modcommunity/how-to-install-mods-in-h3vr/pulls) on this guide's GitHub repository.

Join our [Discord server](https://discord.moddingcommunity.com) if you have any questions or want help with anything modding related!
