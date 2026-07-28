---
icon: lucide/file-sliders
title: AbioticSchema
description: Create and modify DataTable rows with JSON.
---

AbioticSchema is a tool included with AbeLoader that allows mods to easily add, change, replace or remove data from Abiotic Factor's many "datatables".

!!! question "What is a Datatable?"
    Datatables are objects used by Unreal Engine to store large amounts of information in a tidy way. <br>They work like a spreadsheet, with each entry being a single "row". The "columns" in each datatable are defined by something called a `struct`. <br><br>Abiotic Factor uses a large amount of datatables to store info about all kinds of things; items, recipes, loot, NPCs, buffs and many more.

Instead of overwriting datatables with .pak mods, or modifying them with UE4SS Lua, AbioticSchema allows modders to describe their changes in patch files written in JSON. AbeLoader will read `.json` files from a mod's folder, ensure everything is correct, and then apply the patches to each datatable at the correct time.

This approach has a bunch of benefits:

1. Schema mods are **less likely to break your game when it updates.** The previous approach of overwriting datatables often led to missing items, recipes, etc.
2. **Better compatibility when using multiple mods.** Two mods can make changes to the same datatable, which wasn't possible with the previous approach.
3. **Easier for modders.** On top of not needing to repack your mod every update, learning to mod datatables is much easier. AbioticSchema includes settings for VS Code, which will highlight errors in your `.json` files and tell you exactly what is required.

Want to get started? Proceed to the [setup guide](getting_started/setup.md)!