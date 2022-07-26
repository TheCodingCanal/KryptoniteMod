# Minecraft But With {You Decide}! Let’s Mod You Some Minecraft ⚒️🧱

Minecraft is the beloved game by many kids and adults like me for doing almost anything you want in a low res world. The modding community took that idea even further and allowed players to do even more. I love playing modpacks like Feed The Beast that combine a bunch of great mods that give you the ability to cast magic with ruins, travel to other planes, make nuclear reactors, and so much more. Maybe you’ve thought about some cool stuff you’d like to have or do in minecraft to make it even more fun. Well now you can by making your own mod. We’re going to be making our own simple mod, which will set the stage for you to build your own blocks, crafting recipes, tools, armor, mobs, game rules, etc. There’s a lot that we need to do to get to the point of playing our mod and I will guide you step by step in this workshop.

## Table of Contents
- [Download Forge](#Download-Forge)
- [Build With Gradle](#Build-With-Gradle)
- [Running Project, Starting Client](#Running-Project-by-Starting-Client)
- [Introduction](#Introduction)
- [Setting up IDE](#Setting-up-IDE)
- [Building Our Mod](#Building-Our-Mod)
- [Adding our kryptonite ingot](#Adding-our-kryptonite-ingot)
- [Adding Kryptonite Blocks](#Adding-Kryptonite-Blocks)
- [Loot and Tables](#Recipes-and-Loot)
- [Thanks for Coming](#Thanks-for-Coming!)

## Kryptonite Mod
Based on Modding by Kaupenjoe’s [tutorial for v1.19 of Minecraft](https://www.youtube.com/watch?v=LpoSy091wYI&list=PLKGarocXCE1HrC60yuTNTGRoZc6hf5Uvl)

**We're going to jump into the tutorial so we can get everything running and downloading while I give my intro**

Prerequisites:
- Download and install Minecraft - java edition v1.19: use microsoft store
- Download [JDK version 17](https://adoptium.net/temurin/releases/?version=17)
- Download and install either IntelliJ (preferred), Eclipse, or Visual Studio Code
    - If using Eclipse you might need to [install a plugin](https://github.com/sebthom/extra-syntax-highlighting-eclipse-plugin) for editing json files with good syntax highlighting 
- Helpful to know Git for downloading tutorial files
- I would highly suggest a clipboard manager like the built in one to windows or Ditto
## Download Forge
Different options to get the forge files:
- Git clone from this repo using [branch 1-BuildWithGradle](https://github.com/TheCodingCanal/KryptoniteMod/tree/1-BuildWithGradle)
- Download Forge zip from my [google drive](https://drive.google.com/drive/folders/10EA8TrcMEiE2hjJkNC0sB3BwYUyGtYVj?usp=sharing)
- You can download other versions from [Forge](https://files.minecraftforge.net/net/minecraftforge/forge/) directly but it’s very spammy

After you get the files:
1. Unzip, rename, and put in workspace
2. Delete any .txt files
3. Open project with editor of choice (Eclipse needs File > Import > Gradle > Existing Gradle Project)
## Build With Gradle

### Eclipse Import Project and Gradle Build

File > Import > Gradle > Existing Gradle Project

![Eclipse Import Project](https://i.imgur.com/64IDJRu.png)

Go down to Gradle Tasks and click on forgegradle runs > genEclipseRuns

![Eclipse Gradle Build](https://i.imgur.com/xx5C21y.png)

### IntelliJ Open Project and Gradle Build

Open project. The first Gradle build will start when opening project

![Gradle finished building](https://i.imgur.com/uN2mXkB.png)

Go to Gradle tab > Tasks > forgegradle runs > genIntellijRuns

![GenIntelliJRuns](https://i.imgur.com/v0GXMjc.png)

### Visual Studio Code or any editor

Can run these from command line as well
```
./gradlew genEclipseRuns or ./gradlew genVSCodeRuns or ./gradlew genIntellijRuns
```

## Running Project by Starting Client

Then run *runClient*. You can hit Play after this instead of *runClient*

![Eclipse Gradle Run Client](https://i.imgur.com/FJOVrcn.png)

**Let's make sure we can get minecraft started before continuing.** This is the default example mod we will be replacing

![Minecraft running with Example Mod](https://i.imgur.com/r3OnICr.png)

Let's create a new world as well.

## Special Thanks to That Conference and All the Sponsors!

![Sponsors](https://i.imgur.com/yeQN7Mp.png)

## Introduction

### Jesse Dahir-Kanehl

- Developer
- Tinkerer
- Gardener
- Climber
- Cyclist
- Player of modded minecraft

You can reach me on all platforms @TheCodingCanal or send an email to thecodingcanal@gmail.com

Our mod is based on the kryptonite gem. You can replace that with whatever you'd like and make your own mod.

We'll be using Forge. Forge is a framework for building mods. An alternative would be [Fabric](https://fabricmc.net/) which is lighter weight but seems to have less mods using it.

Pay attention to the version when looking at documentation and other tutorials/blogs. Things change and some info is no longer correct. Try to stick to recent sources that use 1.19 or 1.18.x

## Setting up IDE

### Check Java version
IntelliJ 
- File > Project Structure
![Project Structure](https://i.imgur.com/DqwbDZY.png)
- File > Settings > Build, Execution, Deployment > Build Tools > Gradle
![Gradle JDK](https://i.imgur.com/OnUD2ww.png)

### Tree Appearance
IntelliJ
- Right click on gear icon in left navigation menu > Tree Appearance > Unclick Flatten Packages and Compact Middle Packages
![Tree Appearance](https://i.imgur.com/nOLFizV.png)

## Building Our Mod
### The build.gradle file
In parent directory
1. Change version number
2. Change the group name
3. Change the Mod Id and ArchiveBaseName. **Mod Id must be all lowercase, can contain numbers, hyphen, and underscore, but no other special characters. Keep it simple!!**
4. Replace "examplemod" with "kryptonitemod"
    ```
    version = '0.0.1-1.19'
    group = 'com.codingcanal.kryptonitemod' // http://maven.apache.org/guides/mini/guide-naming-conventions.html
    archivesBaseName = 'kryptonitemod'
    ```

### The ExampleMod.java file
Navigate to src > main > java > com.example.examplemod > ExampleMod.java
1. Delete lines 37 through 44. We'll be setting up these functions in other classes to have better organization
    ```
    public static final DeferredRegister<Block> BLOCKS = DeferredRegister.create(ForgeRegistries.BLOCKS, MODID);
    // Create a Deferred Register to hold Items which will all be registered under the "examplemod" namespace
    public static final DeferredRegister<Item> ITEMS = DeferredRegister.create(ForgeRegistries.ITEMS, MODID);

    // Creates a new Block with the id "examplemod:example_block", combining the namespace and path
    public static final RegistryObject<Block> EXAMPLE_BLOCK = BLOCKS.register("example_block", () -> new Block(BlockBehaviour.Properties.of(Material.STONE)));
    // Creates a new BlockItem with the id "examplemod:example_block", combining the namespace and path
    public static final RegistryObject<Item> EXAMPLE_BLOCK_ITEM = ITEMS.register("example_block", () -> new BlockItem(EXAMPLE_BLOCK.get(), new Item.Properties().tab(CreativeModeTab.TAB_BUILDING_BLOCKS)));
    ```

2. Delete blocks and items regsiter
    ```
    // Register the Deferred Register to the mod event bus so blocks get registered
    BLOCKS.register(modEventBus);
    // Register the Deferred Register to the mod event bus so items get registered
    ITEMS.register(modEventBus);
    ```

3. Change the Mod Id
    ```
    package com.codingcanal.kryptonitemod;
    @Mod(KryptoniteMod.MODID)
    public class KryptoniteMod
    {
        // Define mod id in a common place for everything to reference
        public static final String MODID = "kryptonitemod";
    ```

4. Rename file. Click on file and hit Shift + F6 or Right click > Refactor > Rename
![Renaming File](https://i.imgur.com/5FyA94I.png)
5. Change the package name from com.example.examplemod to your package name. Rename packages and delete out old packages

![Renaming Directories](https://i.imgur.com/lqnwCSn.png)


### The mods.toml file
In src > main > resources > META-INF > mods.toml
1. Change license. MIT License suggested
2. Change modId
3. Change version
4. Change displayName

```
# The license for you mod. This is mandatory metadata and allows for easier comprehension of your redistributive properties.
# Review your options at https://choosealicense.com/. All rights reserved is the default copyright stance, and is thus the default here.
license="MIT License"
# A URL to refer people to when problems occur with this mod
#issueTrackerURL="https://change.me.to.your.issue.tracker.example.invalid/" #optional
# A list of mods - how many allowed here is determined by the individual mod loader
[[mods]] #mandatory
# The modid of the mod
modId="kryptonitemod" #mandatory
# The version number of the mod - there's a few well known ${} variables useable here or just hardcode it
# ${file.jarVersion} will substitute the value of the Implementation-Version as read from the mod's JAR file metadata
# see the associated build.gradle script for how to populate this completely automatically during a build
version="0.0.1-1.19" #mandatory
 # A display name for the mod
displayName="Kryptonite Mod" #mandatory
```

Come back to this file before you publish this for other people and flesh out the extra details to have better documentation

### Hit Play and Publish
1. Hit Play! You've got your own mod!!!
![Your Mod](https://i.imgur.com/LeivJwj.png)
2. To build for publishing
    - Gradle tab > Tasks > build > build
    - or put this into the terminal 
    ```
    ./gradlew build
    ```
3. Find jar file in build > libs folder

At this point your project should look something like branch [2-BuildingOurMod](https://github.com/TheCodingCanal/KryptoniteMod/tree/2-BuildingOurMod)

## Adding our kryptonite ingot
### The ModItems file
1. Add item package under kryptonitemod
2. Add ModItems.java file and add to git if using that
3. Add DeferredRegister ITEMS
    - Rememeber to hit tab to autofill and auto add imports
    ```
    public static final DeferredRegister<Item> ITEMS =
            DeferredRegister.create(ForgeRegistries.ITEMS, KryptoniteMod.MODID);
    ```
4. Register ITEMS on the eventBus
    ```
    public static void register(IEventBus eventBus) {
        ITEMS.register(eventBus);
    }
    ```
5. Register ModItems on the modEventBus in **KryptoniteMod.java**
    ``` 
    ModItems.register(modEventBus);
    ```
6. Add RegistryObject KRYPTONITE
    - Can add more items by copying this line
    - Many many different properties to use to configure your items. We will come back to this
    - ![So many properties](https://i.imgur.com/KSbzHAf.png)
    ```
    public static final RegistryObject<Item> KRYPTONITE = ITEMS.register("kryptonite",
            () -> new Item(new Item.Properties().tab(CreativeModeTab.TAB_MISC)));
    ```
7. Add KRYPTONITE_INGOT
    ```
    public static final RegistryObject<Item> KRYPTONITE_INGOT = ITEMS.register("kryptonite_ingot",
            () -> new Item(new Item.Properties().tab(CreativeModeTab.TAB_MISC)));
    ```

### Adding asset directories to our Resources
1. Add directories to match this (might be easier to use File Explorer with Ctrl + Shift + N):
    - ![Asset directories](https://i.imgur.com/5mPEyov.png)
2. Add en_us.json in lang folder
    - Add kryptonite_ingot and kryptonite's display names
    ```
    {
    "item.kryptonitemod.kryptonite": "Kryptonite",
    "item.kryptonitemod.kryptonite_ingot": "Kryptonite Ingot",
    }
    ```
3. Add kryptonite.json in models > item folder
    - Configure texture
    ```
    {
        "parent": "item/generated",
        "textures": {
            "layer0": "kryptonitemod:item/kryptonite"
        }
    }
    ```
4. Add kryptonite_ingot.json in same folder by copying it (select and hit F5)
    ```
    {
    "parent": "item/generated",
    "textures": {
        "layer0": "kryptonitemod:item/kryptonite_ingot"
    }
    }
    ```
5. Add texture files as png's:
    - Use those provided in the [google drive folder](https://drive.google.com/drive/folders/1BsLJ9lTH-YIzMHom8alh1Wun4ggR8Q04?usp=sharing)
    - Can make your own an online editor like [Nova Skin](https://minecraft.novaskin.me/resourcepacks)
    - Or use the External Libraries (Gradle: net.minecraft.client.extra > client-extra.jar > assets > minecraft > textures) and then use Paint, Gimp, etc to edit
        - ![Exteranl Libraries textures](https://i.imgur.com/Aw03Xxc.png)
6. Let's test it out!

At this point your project should look something like branch [3-AddingKryptoniteIngots](https://github.com/TheCodingCanal/KryptoniteMod/tree/3-AddingKryptoniteItems)

## Adding Kryptonite Blocks
### The ModBlocks.java file
1. Add DeferredRegister BLOCKS
    ```
    public static final DeferredRegister<Block> BLOCKS =
            DeferredRegister.create(ForgeRegistries.BLOCKS, KryptoniteMod.MODID);
    ```
2. Register BLOCKS on the event bus
    ```
    public static void register(IEventBus eventBus) {
        BLOCKS.register(eventBus);
    }
    ```
3. Register ModBlocks on the modEventBus in **KryptoniteMod.java**
    ```
    ModBlocks.register(modEventBus);
    ```
4. Create registerBlock function. These are helper functions
    ```
    private static <T extends Block> RegistryObject<T> registerBlock(String name, Supplier<T> block, CreativeModeTab tab) {
        RegistryObject<T> toReturn = BLOCKS.register(name, block);
        return toReturn;
    }
    ```
5. Register block items as well. Blocks are items as well and need to be registered as such
    ```
    private static <T extends Block> RegistryObject<Item> registerBlockItem(String name, RegistryObject<T> block, CreativeModeTab tab) {
        return ModItems.ITEMS.register(name, () -> new BlockItem(block.get(), new Item.Properties().tab(tab)));
    }
    ```
6. Call registerBlockItem method from registerBlock
    ```
    registerBlockItem(name, toReturn, tab);
    ```
7. Register Kryptonite Block
    - Many materials to choose from which give it the correct sounds and visuals
    - Strength of 3f (float) sets how long it takes to mine
    - Currently won't drop any items until we configure the loot json files
    - ![Many properties to use](https://i.imgur.com/wZontXY.png)
    ```
    public static final RegistryObject<Block> KRYPTONITE_BLOCK = registerBlock("kryptonite_block",
            () -> new Block(BlockBehaviour.Properties.of(Material.CACTUS)
                    .strength(3f).requiresCorrectToolForDrops()), CreativeModeTab.TAB_MISC);
    ```
8. Register kryptonite ores
    - Use DropExperienceBlock instead of regular
    - Will give random amount experience between 3 and 6
    - Feel free to change things up to test out these properties and methods
    ```
    public static final RegistryObject<Block> KRYPTONITE_ORE = registerBlock("kryptonite_ore",
            () -> new DropExperienceBlock(BlockBehaviour.Properties.of(Material.STONE)
                    .strength(5f).requiresCorrectToolForDrops(),
                    UniformInt.of(3, 6)), CreativeModeTab.TAB_MISC);
    public static final RegistryObject<Block> DEEPSLATE_KRYPTONITE_ORE = registerBlock("deepslate_kryptonite_ore",
            () -> new DropExperienceBlock(BlockBehaviour.Properties.of(Material.STONE)
                    .strength(6f).requiresCorrectToolForDrops(),
                    UniformInt.of(4, 8)), CreativeModeTab.TAB_MISC);
    ```

### Kryptonite block assets
1. Create kryptonite_block.json, kryptonite_ore.json, and deepslate_kryptonite_ore.json in blockstates
    - This defines the different states and variants for your block
    - More info can be found in the [Forge docs](https://docs.minecraftforge.net/en/1.12.x/models/using/#block-models)
    ```
    {
        "variants": {
            "": { "model":  "kryptonitemod:block/kryptonite_block" }
        }
    }
    ```
2. Create kryptonite_block.json, kryptonite_ore.json, and deepslate_kryptonite_ore.json in models > block
    - Using a cube texture with a single texture file for all sides
    ```
    {
        "parent": "block/cube_all",
        "textures": {
            "all": "kryptonitemod:block/kryptonite_block"
        }
    }
    ```
3. Create kryptonite_block.json, kryptonite_ore.json, and deepslate_kryptonite_ore.json in models > item
    - refer to block model
    ```
    {
    "parent": "kryptonitemod:block/kryptonite_block"
    }
    ```
4. Add our blocks' display names to en_us.json in lang folder
    ```
    "block.kryptonitemod.kryptonite_block": "Block of Kryptonite",
    "block.kryptonitemod.kryptonite_ore": "Kryptonite Ore",
    "block.kryptonitemod.deepslate_kryptonite_ore": "Deepslate Kryptonite Ore"
    ```

Make sure assets looks like this
![Assets for blocks](https://i.imgur.com/HHYE9ur.png)

Let's run it.
Possible errors: 
- Texture works when placed in world but not in inventory > item model json
- Texture works in inventory but not when placed in world > check blockstates json
![Error in code texture](https://i.imgur.com/2DlLXt3.png)
- Doesn't work anywhere. Could be in any of the json files or a bad directory setup and you might have multiple errors

For more ideas and examples look at the external libraries and copy and extend existing blocks

At this point your project should look something like branch [4-AddingKryptoniteBlocks](https://github.com/TheCodingCanal/KryptoniteMod/tree/4-AddingKryptoniteBlocks)

## Recipes and Loot
### Add Data with Recipes
1. Add data folder with subfolders like this:
    - ![data folders](https://i.imgur.com/ayKlR2w.png)
2. Add crafting recipe for kryptonite block
    - pattern can use any key you want and can include multiple items
3. Add other recipes for smelting, blasting, and turning blocks back into ingots

### Loot Tables
1. Add blocks folder under loot tables
2. Add files for each block
    - [Wiki doc for loot table](https://minecraft.fandom.com/wiki/Loot_table)
    - Ores act differently if you have silk touch or just a regular pickaxe

### Adding tags
1. Setup folders under data folder to match this:
    - ![folder structure for tags](https://i.imgur.com/oZKOPgP.png)
2. Add needs_iron_tool.json under blocks folder
    - you might want to later add files for diamond and stone tools
3. Add pickaxe.json under mineable folder
    - you might want to later add files for other tools (shovel, axe, hoe, shears, etc)

Lets test it out. Mine some ore, smelt it, craft a block

At this point your project should look something like branch [5-RecipesAndLoot](https://github.com/TheCodingCanal/KryptoniteMod/tree/5-RecipesAndLoot)


Looking at other mods might help give you ideas and allow you to learn more about what you can do with a mod. For example, check out a fun but simple mod [Iron Chests 2](https://github.com/TechnoVisionDev/IronChest)

## Thanks for Coming!
Join us on That.us and the That Slack!

![Join us on THat.us](https://i.imgur.com/w7F8l2y.png)

Join us in person next year, July 2023!

![Next Year](https://i.imgur.com/l1GU45T.png)