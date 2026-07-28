---
title: AbioticRecipe
---

This struct is used to define recipes. There are three different datatables that use it.

## List of Recipe Datatables

| Datatable | Description |
| :-------- | :---------- |
| <span style="white-space:nowrap">`DT_Recipes`</span>          | Every recipe in the crafting menu, at the Crafting Bench, or the Chef's Counter. |
| <span style="white-space:nowrap">`DT_SoupRecipes`</span>      | Recipes for soup pots. These also get a compendium entry in the "soup recipes" section. |
| <span style="white-space:nowrap">`DT_ChemistryRecipes`</span> | Recipes made at the Chemistry Bench. |

## Recipe Data

This example will focus on DT_Recipes. DT_SoupRecipes and DT_ChemistryRecipes have some unique quirks to them, see the examples below for more info.

```json title="Example recipe data"
{
    "example_recipe": {
        "Table": "DT_Recipes",
        "Mode": "Add",
        "RowData": {
            "ReleaseGroup": {"Enum": ""},
            "ItemToCreate": {"Table": "ItemTable_Global", "Row": "scrap_metal" },
            "CountToCreate": 4,
            "Category": {"Enum": "Resource"}, // Crafting menu category
            "RecipeItems": [
                {"Count": 2, "Item": {"Table": "ItemTable_Pickups", "Row": "scrap_metal"}},
                {"Count": 1, "Item": {"Table": "ItemTable_Global", "Row": "scrap_bio"}}
            ],
            "BenchesRequired": [
                {"Table": "ItemTable_Global", "Row": "Deployable_Bench_Crafting"}
            ],
            "CraftDuration": 10.0,
            "LinkedRecipesToUnlock": [
                {"Table": "DT_Recipes", "Row": ""},
                {"Table": "DT_Recipes", "Row": ""}
            ],
            "NotUnlockableByPickup": true,
            "ResearchData": { // Research minigame
                "MinigameDifficulty": {"Enum": "Easy"},
                "FakeItems": [
                    {"Table": "ItemTable_Pickups", "Row": "screws"},
                    {"Table": "ItemTable_Pickups", "Row": "scrap_plastic"}
                ]
            },
            "StatModifier": {"Row": ""}, //Row name in DT_StatModifiers that will modify the crafting speed. Currently only used by "AmmoCraftingSpeed_Multiply"
            "RecipeTags": []
        }
    }
}
```

### Example Soup

Soup recipes are unique, as they use the `Recipe.Soup` tag and use `"FULLWATERPOT"` in `ItemTable_Global` to represent the full pot of water.

If adding a custom soup item using this recipe, note that the recipe should make a "raw" soup with `CookableData` that will cook it into the actual soup.
Otherwise it will cook instantly upon adding all the ingredients.

```json title="Custom soup recipe"
{
    "custom_soup_recipe": {
        "Table": "DT_SoupRecipes",
        "Mode": "Add",
        "RowData": {
            "CountToCreate": 1,
            "ItemToCreate": { "Table": "ItemTable_Global", "Row": "mod_soup_raw" },
            "Category": { "Enum": "Food" },
            "RecipeTags": ["Recipe.Soup"],
            "RecipeItems": [
                { "Count": 1, "Item": { "Table": "ItemTable_Global", "Row": "FULLWATERPOT" } },
                { "Count": 1, "Item": { "Table": "ItemTable_Global", "Row": "salt" } },
                { "Count": 1, "Item": { "Table": "ItemTable_Global", "Row": "bio_scrap" } },
                { "Count": 1, "Item": { "Table": "ItemTable_Global", "Row": "scrap_metal" } }
            ]
        }
    }
}
```

### Example Chemistry

todo