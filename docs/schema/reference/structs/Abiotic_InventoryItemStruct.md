---
title: InventoryItem
---

Abiotic Factor has a lot of items. These exist across 11* different datatables, called `ItemTables`, that live in `/Game/Blueprints/Items/`

An item can be a lot of different things. Weapons, armor, food, crafting materials, furniture, just to name a few. Because of this, the format of an `InventoryItem` is probably the most complex in the game, and a `.json` file for a single item has roughly **115** different values you can change.

Don't be intimidated, as most of these values are only used for specific kinds of items, and **can be safely ignored** or omitted if you don't need them. For example, if you're adding a new pistol, you probably don't need to add any of the `CookableData` values. Some example items are also included at the bottom of the page.

## List of ItemTables

| ItemTable                               | Description                                                                               |
| :-------------------------------------- | :---------------------------------------------------------------------------------------- |
| `ItemTable_FoodAndGibs`                 | Food, fish, soup, etc. Also anything you get from chopping-up enemies (e.g. skulls, arms) |
| `ItemTable_Weapons`                     | Melee, guns, throwing weapons, shields. Also includes tools like screwdrivers and fishing rods, |
| `ItemTable_Pickups`                     | Many crafting materials. Ammo. Most seeds. Stuff you loot in the world. |
| `ItemTable_Deployables_Small`           | Small deployables. Mostly decorative. |
| `ItemTable_Deployables`                 | Deployables. Furniture, etc. |
| `ItemTable_Deployables_CraftingBenches` | All the crafting tables. |
| `ItemTable_Gear`                        | Armor, backpacks and trinkets. |
| `ItemTable_Plants`                      | Plants, but specifically when planted in the ground. Not to be confused with the food items in `ItemTable_FoodAndGibs` |
| `ItemTable_Craftables`                  | Very big one. Includes everything you can craft. |
| `ItemTable_Pets`                        | All of the pets in held-item form. |
| **`ItemTable_Global`**                  | See below! |

!!! note "**ItemTable_Global**"
    This table is special. It's a `CompositeDataTable`, which in this case is a copy of every other `ItemTable` rolled into one. Most vanilla game logic seems to just read from `ItemTable_Global`. The important info here is that.
    
    1. If you change/add/remove something from any other `ItemTable`, AbioticSchema will automatically mirror those changes in `ItemTable_Global`
    2. If you want to reference an ItemTable in a [Row Reference](), you can safely use `ItemTable_Global` as the `table`.
    3. You can also just change/add/remove from `ItemTable_Global` directly, but changes will not be mirrored in their respective tables. The effects of this haven't been tested, so keep this in mind if you're editing vanilla rows.

## InventoryItem Data

Here is an example patch to add an InventoryItem. Six values have been trimmed, as they all have a lot of other values within them and will be easier to understand if you see them separately.

```json title="Example item with certain values trimmed"
{
    "test": {
        "Table": "ItemTable_Global",
        "Mode": "Add",
        "RowData": {
            "Name": "",
            "Description": "",
            "Flavor": "",
            "ToInteract": "",
            "ToLongPackage": "",
            "ToPackage": "",
            "InventoryIcon": {"Path": ""},
            "ItemClass": {"Path": ""},
            "WorldStaticMesh": {"Path": ""},
            "WorldSkeletalMesh": {"Path": ""},
            "WorldSkeletalAnim": {"Path": ""},
            "DeployedItemClass": {"Path": ""},
            "DeployHologramMesh": {"Path": ""},
            "ScaleWorldMesh": 1.0,
            "ScaleFirstPersonMesh": 1.0,
            "ScaleTPHeldMesh": 1.0,
            "ScaleCooking": 1.0,
            "ScaleHologram": 1.0,
            "CanLoseDurability": false,
            "MaxItemDurability": 10.0,
            "ChanceToLoseDurability": 1.0, //1.0 = 100%, 0.25 = 25%
            "RepairItem": {(Trimmed for example)},
            "StackSize": 1,
            "Weight": 1.0,
            "TryPlaceInHotbar": true,
            "IsWeapon": false,
            "WeaponData": {(Trimmed for example)},
            "EquipmentData": {(Trimmed for example)},
            "ReleaseGroup": {"Enum": ""},
            "PlacementOrientationsAllowed": {"Enum": ""},
            "FPAnimationData": {"Table": "", "Row": ""},
            "FPAttachSocket": "",
            "TPAttachSocket": "",
            "SalvageData": {"Table": "DT_Salvage", "Row": ""}, //The loot you will get from salvaging the item
            "ItemUseFlags": [ //Restrict using an item under certain conditions (eg. military guns without milspec)
                {"Table": "DT_ItemUseFlags", "Row": ""}, 
                {"Table": "DT_ItemUseFlags", "Row": ""}
            ],
            "TextureVariant": {"Table": "DT_TextureVariants", "Row": ""}, //The DT_TextureVariants row for this item, if applicable
            "ConsumableData": {(Trimmed for example)},
            "CookableData": {(Trimmed for example)},
            "LiquidData": {(Trimmed for example)},
            "GameplayTags": []
        }
    }
}
```

### RepairItem

RepairItem defines the item used to repair this item. For some reason it uses the same data structure as `DT_Salvage` (ie. enemy loot tables). As such, most of the values
are unused and `Item` is the only one actually required.

```json
"RepairItem": {
    "Item": {"Table": "ItemTable_Global", "Row": "scrap_metal"}, //required for RepairItem
    "ChanceToDrop": 1.0, //unused
    "QuantityMax": 1, //likely unused
    "QuantityMin": 1, //likely unused. might define quantity needed to repair? needs testing
    "MaxDropQuery": { //unused
        "Op": "ANY_TAGS",
        "Expressions": [],
        "Tags": []
    }
}
```

### WeaponData

WeaponData holds a lot of combat-related values. `"Skeletal"`, `"FireSound` and `"TpAnimation"` are also occasionally used for non-weapon items, such as the equippable watches.

```json
"WeaponData": {
    "Melee": false,
    "MeleeSwingData": {"Table": "DT_MeleeSwingStyles", "Row": ""}, //melee animations
    "TimeBetweenShots": 1.0,
    "MaxHitscanRange": 1.0,
    "DamagePerHit": 1.0,
    "SpreadMin": 1.0,
    "SpreadMax": 1.0,
    "Recoil": 1.0,
    "PelletCount": 1,
    "MagazineSize": 10,
    "RequireAmmo": true,
    "AmmoType": {"Table": "ItemTable_Global", "Row": "ammo_9mm"},
    "AmmoTypes": [
        {"Table": "ItemTable_Global", "Row": "ammo_9mm"},
        {"Table": "ItemTable_Global", "Row": "scrap_plastic"} //can use any item
    ], //assumed mutually exclusive from AmmoType
    "TpAnimation": {"Table": "DT_TPAnimations", "Row": ""}, //third person animation
    "SecondaryAttack": {"Enum": "AimDownSights"},
    "LoudnessPrimary": 1.0,
    "LoudnessSecondary": 1.0,
    "UnderwaterUsage": {"Enum": "Allowed"},
    "BurstFireCount": 2,
    "MaxAimCorrection": 1.0,
    "TracerPerShots": 1,
    "ProjectileClass": {"Path": "/Game/Blueprints/Projectiles/Projectile_Disc.Projectile_Disc_C"}, //path to child of AbioticProjectile_ParentBP_C
    "FireSound": {"Path": "/Game/Audio/Guns/RocketLauncher/S_RL_Fire_Cue.S_RL_Fire_Cue"}, //path to valid SoundCue
    "HitscanDamageType": {"Path": "/Game/Blueprints/DamageTypes/DamageType_Fire_Holy.DamageType_Fire_Holy_C"}, //path to valid damage type class
    "Skeletal": {
        "Animation": {"Table": "DT_WeaponAnimationData", "Row": ""}, //row that contains the animation data
        "Mesh": {"Path": ""} //the skeletal mesh of the weapon. used for meshes that have custom animations eg. guns reloading, construction gauntlet
    },
    "AmmoVisuals": {
        "Mesh": {"Path": ""}, //mesh to attach to the weapon when ammo is loaded
        "Visuals": { //alternative to "Mesh" that takes a socket name and then the mesh, used for crossbow bolts and fishing rod bait in vanilla
            "xbowboltsocket": {"Path": ""}
        }
    }
}
```

### EquipmentData

EquipmentData holds values related to equippable items (armor, trinkets, backpacks, etc).

```json
"EquipmentData": {
    "EquipSlot": {"Enum": "Backpack"},
    "CanAutoEquip": true,
    "ArmorBonus": 3,
    "HeatResist": 1,
    "ColdResist": 1,
    "DamageMitigationType": { //Map key is a valid damage type class, value is the dmg reduction represented by a double
        "/Game/Blueprints/DamageTypes/DamageType_Explosive.DamageType_Explosive_C": 0.75, //0.75 = 75% dmg reduction
        "/Game/Blueprints/DamageTypes/DamageType_Sharp.DamageType_Sharp_C": 0.10 //0.10 = 10% dmg reduction
    },
    "IsContainer": true,
    "ContainerCapacity": 12,
    "ContainerWeightReduction": 0.15, //0.15 = 15% weight reduction
    "InventoryPlaceSound": {"Path": ""},
    "SetBonus": {"Row": ""} //Hardcoded to a row in DT_SetBonuses
}
```

### ConsumableData

ConsumableData holds values related to food and other consumables. `BuffsToAdd` is also used for equipment that grant buffs when equipped, and `Radioactivity` is used for any radioactive item.

```json
"ConsumableData": {
    "TimeToConsume": 1.0,
    "ThirstFill": 15.0,
    "HungerFill": -10.0, //Negative values also work
    "FatigueFill": 5.0,
    "ContinenceFill": 5.0, //Toilet
    "SanityFill": 5.0, //Unused
    "TemperatureChange": 0.0, //Unused
    "RadiationChange": 2.0,
    "HealthChange": 0.0, //Unused
    "ArmorChange": 0.0, //Unused
    "BuffsToAdd": ["Buff_SouperSatisfied", "Buff_Tincture_Giganto"],
    "BuffsToRemove": ["Debuff_LegSprain", "Buff_CrowleysCurse"],
    "ConsumableTag": "",
    "ConsumedAction": "", //Maybe unused?
    "Radioactivity": 0.005
}
```

### CookableData

CookableData holds values related to cooking and farming. `CanItemDecay`, `ItemDecayTemperature` and `DecayToItem` are also used for certain non-food items like Electrical Organs (from eels)

```json
"CookableData": {
    "IsCookware": false,
    "CanBeCooked": true,
    "CookedItem": {"Table": "ItemTable_Global", "Row": ""},
    "BurnedItem": {"Table": "ItemTable_Global", "Row": ""},
    "TimeToCookBase": 45.0, //45.0 = 45 seconds
    "TimeToBurnBase": 20.0,
    "FarmableData": {"Row": ""}, //Hardcoded row in DT_Plants
    "RequiresBaking": false,
    "StartingPortions": 4,
    "CanItemDecay": true,
    "ItemDecayTemperature": {"Enum": "Regular"}, //Temperature this item will decay at
    "DecayToItem": {"Table": "ItemTable_Global", "Row": ""}
},
```

### LiquidData

LiquidData holds values related to liquids. Be aware that "liquids" also includes things like "Battery" and "Laser" (aka. the charge on items like the Laser Katana), so this section is used in a variety of different ways.

```json
"LiquidData": {
    "MaxLiquid": 30,
    "AllowedLiquids": [ //Array of liquids this item can hold
        {"Enum": "Antejuice"},
        {"Enum": "RadioactiveWaste"}
    ],
    "PercentageLiquidStart": 0.50, //0.50 = 50% of MaxLiquid
    "LiquidStart": [ //The liquid this starts with when first obtained
        {"Enum": "Antejuice"}
    ]
},
```

## Example Items

Below are some examples of InventoryItem `.json` files.

### Bio-Fusion Pocketwatch

A custom watch, based on `pocketwatch` in `ItemTable_Pickups`, that applies the **Bio-Fusion Armwraps** buff to the player while equipped.

![bio-fusion pocketwatch](/docs/assets/screenshots/inventoryitem/biofusionwatch.png){width=100%}

```json title="fusion_pocketwatch.json"
{
  "biofusion_watch": {
    "Table": "ItemTable_Global",
    "Mode": "Add",
    "RowData": {
      "Name": "Bio-Fusion Pocketwatch",
      "Description": "An anomalous timepiece that allows the wearer to circumvent a variety of biometric and esoteric locks.",
      "InventoryIcon": { "Path": "/Game/Textures/GUI/ItemIcons/itemicon_pocketwatch_new.itemicon_pocketwatch_new" },
      "WorldStaticMesh": { "Path": "/Game/Models/Items/Misc/SM_PocketWatch.SM_PocketWatch"},
      "StackSize": 1,
      "ItemClass": { "Path": "/Game/Blueprints/Items/Gear/Gear_Watch_ParentBP.Gear_Watch_ParentBP_C" },
      "WorldSkeletalMesh": { "Path": "/Game/Models/Characters/Scientist/FPArms/Watches/PocketWatch/SK_PocketWatch.SK_PocketWatch" },
      "Weight": 0.4,
      "WeaponData": {
        "Skeletal": { 
            "Mesh": { "Path": "/Game/Models/Characters/Scientist/FPArms/Watches/PocketWatch/SK_PocketWatch.SK_PocketWatch"},
            "Animation": { "Table": "DT_WeaponAnimations", "Row": "pocketwatch" }
        }
      },
      "EquipmentData": {
        "CanAutoEquip": true,
        "EquipSlot": { "Enum": "Wristwatch" },
        "InventoryPlaceSound": {"Path": "/Game/Audio/UI/Inventory/item_stash_leather_Cue.item_stash_leather_Cue"}
      },
      "ConsumableData": {
        "BuffsToAdd": [ "Buff_Biometric_t3", "Buff_Pocketwatch" ]
      },
      "FPAttachSocket": "r_gun",
      "TPAttachSocket": "r_item_generic1",
      "GameplayTags": [ "Item.Material.Tech" ]
    }
  }
}
```

### Modifying armor stats

This file modifies the Jinxed Shinplates from the Hex armor set to have increased armor and +1 cold resistance.

![modifying armor](/docs/assets/screenshots/inventoryitem/hexlegs.png){width=100%}

```json title="modified_hex_armor.json"
{
    "armor_legs_hex":{
        "Table": "ItemTable_Gear",
        "Mode": "Merge",
        "RowData": {
            "EquipmentData": {
                "ColdResist": 1,
                "ArmorBonus": 30
            },
            "Description": "I modified this item!"
        }
    }
}
```