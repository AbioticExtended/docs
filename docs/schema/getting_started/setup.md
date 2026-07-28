---
icon: lucide/download
title: Setting up
description: Setting up VS Code and FModel for AFS Modding
---

To get started making mods with AbioticSchema, you'll need three things:

1. A copy of Abiotic Factor [**with UE4SS-AF and ABS installed**](../../users/installing.md)
2. **Visual Studio Code (aka. "VS Code")**
3. **FModel**

This page will cover how to setup **VS Code** and **FModel** for `.json` modding.

## VS Code

This guide assumes you are somewhat familiar with VS Code. If you aren't, it's basically a fancy text editor. AbioticSchema includes a `.vscode` folder, which will be automatically loaded and used by VS Code to provide you with helpful hints and check for errors in your `.json` files.

If you don't have VS Code already, you can download it here: https://code.visualstudio.com/download

![Open folder in VS Code](/docs/assets/screenshots/gettingstarted/vscode.png){width=40% align=right}

With VS Code open, select `File -> Open Folder...` and navigate to the `AbioticSchema` folder in your game installation. This will be somewhere like `steamapps/common/AbioticFactor/AbioticFactor/Binaries/Win64/ue4ss/Mods/AbioticSchema`

Having this folder open in VS Code is all that's required to get started making `.json` mods. But before we get started, we'll walk through how to use **FModel**.

## FModel

FModel is a free program used to datamine Unreal Engine games. Once set up, you'll be able to browse Abiotic Factor's assets, export models/textures/sounds/etc, and examine datatables or blueprints. This is useful for modding, as some `.json` mods will require you to find the location of a specific asset (e.g. a texture).

Being able to view existing datatable rows will also give you a better understanding of how they work, and how to create your own. For example, if I want to create a new pistol I might find the vanilla item datatable row for `security_pistol` and use it as a reference.

You can download FModel from here: https://fmodel.app/

![FModel start menu](/docs/assets/screenshots/gettingstarted/fmodel_start.png){width=50% align=right}

With FModel open for the first time, you'll see a window that looks like the one to the right. Select `Add Undetected Game`, enter `AbioticFactor` for the name, and the ==**full path**== to your `steamapps/common/AbioticFactor` folder for the location. Also ensure that ==**UE Versions**== is set to `GAME_UE5_4`, and then click OK.

You should now see `pakchunk0-Windows.pak` and `pakchunk0-Windows.utoc` in the **Archive** tab on the left; these are where the game assets are stored. Before FModel can open these files we need a **"mapping file"**, which will show FModel how to open them correctly. You could generate one of these yourself, but thankfully the modding community has them available to [download here](https://github.com/RevontuletCXVII/AbioticFactor-ModdingCommunity/tree/main/Mapping%20Files). Make sure you download the latest version, and put it somewhere safe.

![FModel settings menu](/docs/assets/screenshots/gettingstarted/fmodel_settings.png){width=80%}
/// caption
///

To load our mapping file, open up FModel's settings, enable `Local Mapping File` and enter the path to the `.umap` file you just downloaded. While not part of this guide, you may also wish to enable `Serialize Script Bytecode` and `Decompile Blueprints to Pseudo C++` if you'd like to try more advanced "blueprint mods" in the future.

### Using FModel

With everything correctly setup, you should now be able to open the files listed in the **Archive** tab. Most of the game's assets are inside `pakchunk0-Windows.utoc`. FModel is able to browse through these files just like a regular file explorer. The game's datatables live in `AbioticFactor/Content/Blueprints/DataTables` and `AbioticFactor/Content/Blueprints/Items`, but feel free to explore and get familiar with where other things are.

![FModel browser](/docs/assets/screenshots/gettingstarted/fmodel_using.png){width=80%}
/// caption
///

In the next part of this guide, we'll cover how to create the folder our mod files will be placed in.