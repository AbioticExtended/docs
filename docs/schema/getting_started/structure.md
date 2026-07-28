---
icon: lucide/clipboard-check
title: Structuring our mod
description: Learning about mod structure.
---

![Open folder in VS Code](/docs/assets/screenshots/gettingstarted/code.gif){width=40% align=right}

With the setup complete, we can finally start modding.<br> In **VS Code**, with the `AbioticSchema` folder open, right click the `mods` folder and create a **new folder** for our tutorial mod.

For AbioticSchema to recognise this folder as something it can load, we need to create a file with some info about our mod.

## Creating a mod.toml

AbioticSchema reads a TOML file placed in each mod's folder to discover what the mod is and if it depends on any other mods.  
Create a `mod.toml` file in your new folder, based on the example below.

```toml title="Example mod.toml file"
modID = "tutorialmod"
version = "1.0.0"
displayName = "My Tutorial Mod"
authors = "Tutorial Person"
```

| Key                       | Description                                                                                                     | Example    |
| :------------------------ | :-------------------------------------------------------------------------------------------------------------- | :--------- |
| `modID`                   | A **unique** ID for your mod. Can only be letters and numbers, case insensitive!                                | `"mymod"`  |
| `version`                 | The mod's version. Any string works, but if you expect other mods to depend on yours it's best to use numbers.  | `"1.0"`    |
| <span style="white-space:nowrap">`displayName`</span> | A friendlier name for your mod. Currently only used for logging.                    | `"My Mod"` |
| `authors`                 | The creators of the mod. Also used for logging.                                                                 | `"Me"`     |

This file is also used to set ==dependencies== for your mod. While not used for this tutorial, see the dropdown below to learn how to use them.

??? info "How to use Dependencies"

    To use dependencies, add any number of `[[dependency]]` sections underneath the main contents of your `mod.toml` file.

    ```toml title="Example mod.toml file with two dependencies"
    modID = "tutorialmod"
    version = "1.0.0"
    displayName = "My Tutorial Mod"
    authors = "Tutorial Person"

    [[dependency]]
    modID = "customizationmod"
    mandatory = true
    ordering = "AFTER"

    [[dependency]]
    modID = "examplemod"
    mandatory = false
    ordering = "BEFORE"
    versionRange = "(1.0,)"
    ```

    | Key            | Description                                                                                          | Example           |
    | :--------------| :--------------------------------------------------------------------------------------------------- | :---------------- |
    | `modID`        | The modID of your mod's dependency.                                                                  | `"examplemod"`    |
    | `mandatory`    | If `true`, your mod will fail to load if this dependency isn't present.                              | `true` or `false` |
    | `ordering`     | Should your mod load `"BEFORE"` or `"AFTER"` this dependency. <br> `"NONE"` if it doesn't matter.    | `"AFTER"`         |
    | <span style="white-space:nowrap">`versionRange`</span> | **(OPTIONAL)** The acceptable version range of the dependency. See below.                            | `"[1.0,2.0)"`     |

    AbioticSchema's `versionRange` uses a format inspired by the Minecraft Forge/Maven one. If omitted from a `[[dependency]]` any version will be accepted.

    ```toml
    # Square brackets include a boundary. Regular parentheses exclude a boundary. 
    # Commas separate minimum and maximum versions.

    versionRange = "[1.0]" # Requires version 1.0 exactly.
    versionRange = "[1.0,2.0)" # Accepts versions from 1.0 up to, but not including, 2.0
    versionRange = "[1.0,)" # Accepts 1.0 and every later version
    versionRange = "(,2.0]" # Accepts 2.0 and every earlier version
    ```  

Now that we have our TOML file, AbioticSchema will recognise the folder as a valid mod it can try to load. However, right now our mod doesn't do anything!
In the next section we'll create our very first datatable edit: **changing a vanilla recipe.**