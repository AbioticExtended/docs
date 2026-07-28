---
icon: lucide/wand-sparkles
title: Changing a recipe
description: Learning how to change a vanilla recipe.
---

Now that your mod has a folder and a `mod.toml` file, we can start adding patches to it. For our first patch, we're gonna tweak a vanilla recipe.

### Where do we put our patch?

![Creating a new folder and file for recipes](/assets/screenshots/gettingstarted/newrecipe.png){width=30% align=right}

AbioticSchema expects patches to be organised into specially-named folders. In other words, all your recipe patches should be in a `Recipes/` folder, all your item patches should be in an `Items/` folder, and so on.

For now, create a `Recipes/` folder in your mod folder. In this folder, create a new `.json` patch file. Patch files can be named whatever you like, so it's a good idea to pick names that will help you remember what each patch does.

!!! info
    If you ever aren't sure what folder a patch should go in, you can find out by reading [the reference guide](../reference/#list-of-datatables)!

### Creating the patch

Open up your `.json` file, and paste this in:

```json
{
    "": {

    }
}
```

This is the JSON object that'll eventually become our patch. But it's missing some stuff. 

#### Finding a row to edit

![Finding a row in FModel](/assets/screenshots/gettingstarted/fmodel_bolts.png){width=40% align=right}

First, we need to find the name of the row we want to edit. I've decided I want this patch to rebalance the crafting recipe for **Makeshift Bolts**. 

After searching through `DT_Recipes` with FModel (CTRL+F is helpful for this), I find the row: `recipe_bolts`

Let's add this to the thing we just pasted into our `.json` file, inside the quote marks.

```json
{
    "recipe_bolts": {

    }
}
```

#### Adding missing properties

![VS Code Warning](/assets/screenshots/gettingstarted/vscode_error.png){width=40% align=right}

At this point, if everything is setup correctly, VS Code should now be complaining about your patch and drawing a squiggly yellow line underneath it. 

This is because the `.vscode` folder tells VS Code what a valid recipe patch should look like, and so it warns you there's some stuff missing.

Let's add the missing properties, and set the `"Table"` to be `DT_Recipes`.

```json
{
    "recipe_bolts": {
        "Table": "DT_Recipes",
        "Mode": "",
        "RowData": {
        }
    }
}
```

#### Setting the patch mode

![VS Code Patch Mode Warning](/assets/screenshots/gettingstarted/vscode_patchmode.png){width=80%}
/// caption
///

You may notice a new yellow line has appeared, warning that we need to choose a **Mode** for the patch. But what is a mode? It just tells the patcher how to behave when handling our patch. For example, `"Merge"` will try to modify an existing row, while `"Add"` will try to add a row only if it doesn't already exist. 

You can learn more about modes in [the reference guide](../reference/#patch-modes), but for this tutorial we'll just use the `"Merge"` mode. This mode is perfect for modifying vanilla content.

```json
{
    "recipe_bolts": {
        "Table": "DT_Recipes",
        "Mode": "Merge",
        "RowData": {
        }
    }
}
```

#### Patching some values

Finally, we can start deciding what we want our patch to change about the row. 

![VS Code being helpful](/assets/screenshots/gettingstarted/vscode_helpful.png){width=40% align=right}

When you type your first quote-mark inside `"RowData"`, VS Code will share some hints about the different properties available. You can learn more about these properties on the dedicated page for [Recipes](../reference/structs/AbioticRecipe_Struct.md).

You can set as many or as few of these properties as you'd like. In my example, I'm just gonna change the cost of the recipe and the amount of bolts I get in return.

Following VS Code's suggestions (and using the Tab key to autocomplete), I ended up with this:

```json
{
    "recipe_bolts": {
        "Table": "DT_Recipes",
        "Mode": "Merge",
        "RowData": {
            "CountToCreate": 24,
            "RecipeItems": [
                {"Item": {"Table": "ItemTable_Global", "Row": "scrap_metal"}, "Count": 1},
                {"Item": {"Table": "/Game/Blueprints/Items/ItemTable_Global.ItemTable_Global", "Row": "pens"}, "Count": 3}
            ]
        }
    }
}
```

Pay close attention to the blocks that look like `{"Table": "", "Row: ""}`, as this is something you'll see across a lot of datatables. These are **Datatable Row References**, which is how datatables can point to rows in other datatables.

In this case, they point to the items in `ItemTable_Global` (a datatable) that will be used for the recipe. `"Table"` can take the full path to the table, or a shorthand alias.

With that, our patch should be ready!

### Seeing it in-game

If everything is correct, we should see our recipe patch applied when we start the game! 

When testing AbioticSchema mods, it's recommended to enable UE4SS's GuiConsole (if it isn't already), as the loader will log every step of the process and let you know if anything goes wrong.

![AFS logging](/assets/screenshots/gettingstarted/afs_logging.png){width=40% align=right}

```ini title="UE4SS-settings.ini"
[Debug]
; Whether to enable the external UE4SS debug console.
ConsoleEnabled = 0
GuiConsoleEnabled = 1
GuiConsoleVisible = 1
```

After loading a save and going to the Crafting Bench, you can see the patch was successful!

![AFS logging](/assets/screenshots/gettingstarted/ingame_recipe.png)

!!! success "Well done!"
    You just made your very first datatable edit. The sky is the limit from here. If you ever get stuck, try to find some examples to reference using FModel, on this wiki, or from other peoples mods.

    The next tutorial will cover how to add a brand new row to a datatable, in the form of a custom item.