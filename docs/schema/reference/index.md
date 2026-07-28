---
icon: lucide/book-marked
title: Schema Reference Sheet
---

This page is the main reference sheet for AbioticSchema.

## Patch Format

A standard `.json` patch file usually looks like this:

```json
{
    "row_name_to_target":{
        "Table": "name of the datatable",
        "Mode": "patch mode you want to use",
        "RowData": {
            row data goes here
        }
    }
}
```

The outer property (`"row_name_to_target"`) will be used to select or create a row in the datatable. If editing a row, you'll want to use its name for this property.
If creating a new row, you should pick something unique.

Depending on the type of datatable you're targeting, the `"Table"` property might not be used. An example is `LevelFX`, where all patches are forced to target `DT_LevelFX`.

#### Patch Modes

`"Mode"` changes how the patcher behaves. Some have more niche use cases than others. You will mostly use `"Auto"` and `"Merge"`.

```json
"Auto", // Patch the row if it exists, add a new row with this data if not
"Add", // Add a row with this data. If the row already exists, cancel.
"Replace", // Remove row if it exists, then add a new row. If row doesn't exist, cancel.
"Merge", // Patch the row if it exists. If row doesn't exist, cancel.
"Remove" // Remove the row if it exists. Does nothing if it does not.
```

## List of Datatables

Abiotic Factor uses a lot of datatables (over 100!). Find all of them below, along with a link to their respective `struct`, and the name of the subfolder you should place your `.json` files in for them.

!!! bug
    If a struct is missing a subfolder in this table, it hasn't been implemented yet. 
    I tried to implement all of the most important ones for now, but if you need something implemented sooner mention it in the discord :)

| Struct | Datatables | Mod Subfolder
| --- | --- | --- |
| [Abiotic_CustomizationStruct](structs/Abiotic_CustomizationStruct.md)                 | `DT_Customization_Beards` `DT_Customization_Belt` `DT_Customization_FannyPacks` `DT_Customization_HairColor` `DT_Customization_HairStyle` `DT_Customization_Head` `DT_Customization_HeadAccessory` `DT_Customization_IDCard` `DT_Customization_Labcoats` `DT_Customization_LowerBody` `DT_Customization_Makeup` `DT_Customization_ShirtColor` `DT_Customization_Shoes` `DT_Customization_Tie` `DT_Customization_UpperBody` `DT_Customization_Watch` | <span style="white-space:nowrap">`/Customization/`</span> |
| [Abiotic_EmailStruct](structs/Abiotic_EmailStruct.md)                                 | `DT_Emails` | |
| [Abiotic_FPAnimationStruct](structs/Abiotic_FPAnimationStruct.md)                     | `DT_FPAnimations` | <span style="white-space:nowrap">`/FPAnimations/`</span> |
| [Abiotic_InventoryItemStruct](structs/Abiotic_InventoryItemStruct.md)                 | `ItemTable_Craftables` `ItemTable_Deployables` `ItemTable_Deployables_CraftingBenches` `ItemTable_Deployables_Small` `ItemTable_FoodAndGibs` `ItemTable_Gear` `ItemTable_Global` `ItemTable_Pets` `ItemTable_Pickups` `ItemTable_Plants` `ItemTable_Weapons` | <span style="white-space:nowrap">`/Items/`</span> |
| [Abiotic_ItemDropTableStruct](structs/Abiotic_ItemDropTableStruct.md)                 | `DT_Salvage` | <span style="white-space:nowrap">`/Salvage/`</span> |
| [Abiotic_NPCStruct](structs/Abiotic_NPCStruct.md)                                     | `DT_NPCList` | <span style="white-space:nowrap">`/NPCList/`</span> |
| [Abiotic_ProjectileStruct](structs/Abiotic_ProjectileStruct.md)                       | `DT_Projectiles` | <span style="white-space:nowrap">`/Projectiles/`</span> |
| [Abiotic_WeaponAnimationData_Struct](structs/Abiotic_WeaponAnimationData_Struct.md)   | `DT_WeaponAnimations` | <span style="white-space:nowrap">`/WeaponAnimations/`</span> |
| [AbioticRecipe_Struct](structs/AbioticRecipe_Struct.md)                               | `DT_ChemistryRecipes` `DT_Recipes` `DT_SoupRecipes` | <span style="white-space:nowrap">`/Recipes/`</span> |
| [Achievement](structs/Achievement.md)                                                 | `DT_Achievements` | |
| [AchievementStat](structs/AchievementStat.md)                                         | `DT_AchievementStats` | |
| [Announcement_Struct](structs/Announcement_Struct.md)                                 | `DT_Announcements` | <span style="white-space:nowrap">`/Announcements/`</span> |
| [ArmorStandPose_Struct](structs/ArmorStandPose_Struct.md)                             | `DT_ArmorStandPose` | |
| [Assault_Struct](structs/Assault_Struct.md)                                           | `DT_Assaults` | <span style="white-space:nowrap">`/Assaults/`</span> |
| [BeaconIcons_Struct](structs/BeaconIcons_Struct.md)                                   | `DT_BeaconIcons` | |
| [BenchUpgrade](structs/BenchUpgrade.md)                                               | `DT_BenchUpgrades` | |
| [BuffDebuff](structs/BuffDebuff.md)                                                   | `DT_BuffsDebuffs` | |
| [CompendiumEntry](structs/CompendiumEntry.md)                                         | `DT_Compendium` | <span style="white-space:nowrap">`/Compendium/`</span> |
| [ConsoleCommand_Struct](structs/ConsoleCommand_Struct.md)                             | `DT_ConsoleCommands` | |
| [DamageDefinition](structs/DamageDefinition.md)                                       | `DT_DamageDefinitions` | <span style="white-space:nowrap">`/DamageDefinitions/`</span> |
| [DebrisData_Struct](structs/DebrisData_Struct.md)                                     | `DT_Debris` | |
| [DistillationEntry_Struct](structs/DistillationEntry_Struct.md)                       | `DT_ItemDistillations` | <span style="white-space:nowrap">`/ItemDistillations/`</span> |
| [Emote_Struct](structs/Emote_Struct.md)                                               | `DT_Emotes` | <span style="white-space:nowrap">`/Emotes/`</span> |
| [ErrorMessage](structs/ErrorMessage.md)                                               | `DT_ErrorMessages` | |
| [FishData](structs/FishData.md)                                                       | `DT_Fish` | <span style="white-space:nowrap">`/Fish/`</span> |
| [FishingZone](structs/FishingZone.md)                                                 | `DT_FishingZones` | <span style="white-space:nowrap">`/FishingZones/`</span> |
| [GameActivity](structs/GameActivity.md)                                               | `DT_GameActivities` | |
| [GameCommand](structs/GameCommand.md)                                                 | `DT_GameCommands` | |
| [GameCredit](structs/GameCredit.md)                                                   | `DT_GameCredits` | |
| [GameEntitlement](structs/GameEntitlement.md)                                         | `DT_GameEntitlements` | |
| [GameSetting](structs/GameSetting.md)                                                 | `DT_AccessibilitySettings` `DT_AudioSettings` `DT_ControlSettings` `DT_GameplaySettings` `DT_VideoSettings` | |
| [HolsterState_Struct](structs/HolsterState_Struct.md)                                 | `DT_HolsterStates` | <span style="white-space:nowrap">`/HolsterStates/`</span> |
| [ItemAction](structs/ItemAction.md)                                                   | `DT_ItemActions` | |
| [ItemCosmetics_Struct](structs/ItemCosmetics_Struct.md)                               | `DT_ItemCosmetics` | <span style="white-space:nowrap">`/ItemCosmetics/`</span> |
| [ItemCountArray_Struct](structs/ItemCountArray_Struct.md)                             | `DT_ResourceList` | |
| [ItemResearchMaterialFrame_Struct](structs/ItemResearchMaterialFrame_Struct.md)       | `DT_ItemResearchFrames` | |
| [ItemUpgrade](structs/ItemUpgrade.md)                                                 | `DT_ItemUpgrades` | <span style="white-space:nowrap">`/ItemUpgrades/`</span> |
| [ItemUseFlag_Struct](structs/ItemUseFlag_Struct.md)                                   | `DT_ItemUseFlags` | |
| [JournalEntry_Struct](structs/JournalEntry_Struct.md)                                 | `DT_JournalEntries` | |
| [JournalMap_Struct](structs/JournalMap_Struct.md)                                     | `DT_MapPamphlets` | |
| [KeybindSetting](structs/KeybindSetting.md)                                           | `DT_KeybindSettings` | |
| [LevelFXData_Struct](structs/LevelFXData_Struct.md)                                   | `DT_LevelFX` | <span style="white-space:nowrap">`/LevelFX/`</span> |
| [LevelMetadata_Struct](structs/LevelMetadata_Struct.md)                               | `DT_Levels` | |
| [MainMenuBackground](structs/MainMenuBackground.md)                                   | `DT_MainMenuBackground` | |
| [NPCConversation](structs/NPCConversation.md)                                         | `DT_NPC_Conversations` | <span style="white-space:nowrap">`/NPCConversations/`</span> |
| [NPCSpawnSubstitute_Struct](structs/NPCSpawnSubstitute_Struct.md)                     | `DT_NPCSpawnSubstitutes` | <span style="white-space:nowrap">`/NPCSpawnSubstitutes/`</span> |
| [NPCTrader](structs/NPCTrader.md)                                                     | `DT_NPC_Traders` | <span style="white-space:nowrap">`/Traders/`</span> |
| [NPCVoice](structs/NPCVoice.md)                                                       | `DT_NPCVoices` | <span style="white-space:nowrap">`/NPCVoices/`</span> |
| [PaintedDeployable](structs/PaintedDeployable.md)                                     | `DT_PaintedDeployables` | <span style="white-space:nowrap">`/PaintedDeployables/`</span> |
| [Pet_Struct](structs/Pet_Struct.md)                                                   | `DT_Pets` | <span style="white-space:nowrap">`/Pets/`</span> |
| [PlantData](structs/PlantData.md)                                                     | `DT_Plants` | <span style="white-space:nowrap">`/Plants/`</span> |
| [QuestData](structs/QuestData.md)                                                     | `DT_Quests` | |
| [RecipeSubstitutes_Struct](structs/RecipeSubstitutes_Struct.md)                       | `ItemTable_RecipeSubstitutes` | |
| [SandboxOption](structs/SandboxOption.md)                                             | `DT_SandboxOptions` | |
| [SetBonus](structs/SetBonus.md)                                                       | `DT_SetBonuses` | <span style="white-space:nowrap">`/SetBonuses/`</span> |
| [SimpleTexture2D_Struct](structs/SimpleTexture2D_Struct.md)                           | `DT_JobBanners` | <span style="white-space:nowrap">`/JobBanners/`</span> |
| [SingleText_Struct](structs/SingleText_Struct.md)                                     | `DT_TeleporterTags` | |
| [SkillData](structs/SkillData.md)                                                     | `DT_Skills` | <span style="white-space:nowrap">`/Skills/`</span> |
| [SkillPerk](structs/SkillPerk.md)                                                     | `DT_SkillPerks` | <span style="white-space:nowrap">`/SkillPerks/`</span> |
| [SkillPerkData_Struct](structs/SkillPerkData_Struct.md)                               | `DT_SkillRecipes` | <span style="white-space:nowrap">`/SkillRecipes/`</span> |
| [StatModifier](structs/StatModifier.md)                                               | `DT_StatModifiers` | |
| [StoryProgress_Struct](structs/StoryProgress_Struct.md)                               | `DT_StoryProgression` | |
| [TextureVariant_Struct](structs/TextureVariant_Struct.md)                             | `DT_TextureVariants` | <span style="white-space:nowrap">`/TextureVariants/`</span> |
| [TPAnimation_Struct](structs/TPAnimation_Struct.md)                                   | `DT_TPAnimations` | <span style="white-space:nowrap">`/TPAnimations/`</span> |
| [TraderItems_Struct](structs/TraderItems_Struct.md)                                   | `DT_NPC_TraderItems` | <span style="white-space:nowrap">`/TraderItems/`</span> |
| [Trait_Struct](structs/Trait_Struct.md)                                               | `CDT_AllTraits` `DT_PhDs` `DT_Traits` | <span style="white-space:nowrap">`/Traits/`</span> |
| [TutorialHint_Struct](structs/TutorialHint_Struct.md)                                 | `DT_TutorialHints` | |
| [TutorialPanelKeybindTips_Struct](structs/TutorialPanelKeybindTips_Struct.md)         | `DT_TutorialPanelKeybindTips` | |
| [TutorialPanelTips_Struct](structs/TutorialPanelTips_Struct.md)                       | `DT_TutorialPanelTips` | |
| [TVTips_Struct](structs/TVTips_Struct.md)                                             | `DT_TVTips` | |
| [UIKeybindAction](structs/UIKeybindAction.md)                                         | `DT_UIKeybindActions` | |
| [UIPopup](structs/UIPopup.md)                                                         | `DT_UIPopups` | |
| [UnderwaterFX_Struct](structs/UnderwaterFX_Struct.md)                                 | `DT_UnderwaterFX` | |
| [WaypointData_Struct](structs/WaypointData_Struct.md)                                 | `DT_Waypoints` | |
| [WeaponCoating_Struct](structs/WeaponCoating_Struct.md)                               | `DT_WeaponCoatings` | <span style="white-space:nowrap">`/WeaponCoatings/`</span> |
| [WeaponMeleeData_Struct](structs/WeaponMeleeData_Struct.md)                           | `DT_MeleeSwingStyles` | <span style="white-space:nowrap">`/MeleeSwingStyles/`</span> |
| [WeatherEvent](structs/WeatherEvent.md)                                               | `DT_WeatherEvents` | <span style="white-space:nowrap">`/Weather/`</span> |
| [WishingShelfStats_Struct](structs/WishingShelfStats_Struct.md)                       | `DT_WishingShelfItems` | |
| [WorldFlag](structs/WorldFlag.md)                                                     | `DT_WorldFlags` | |
| [WorldFlagTrigger](structs/WorldFlagTrigger.md)                                       | `DT_WorldFlagTriggers` | |
