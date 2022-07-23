# Minecraft But With {You Decide}! Let’s Mod You Some Minecraft ⚒️🧱

Minecraft is the beloved game by many kids and adults like me for doing almost anything you want in a low res world. The modding community took that idea even further and allowed players to do even more. I love playing modpacks like Feed The Beast that combine a bunch of great mods that give you the ability to cast magic with ruins, travel to other planes, make nuclear reactors, and so much more. Maybe you’ve thought about some cool stuff you’d like to have or do in minecraft to make it even more fun. Well now you can by making your own mod. We’re going to be making our own simple mod, which will set the stage for you to build your own blocks, crafting recipes, tools, armor, mobs, game rules, etc. There’s a lot that we need to do to get to the point of playing our mod and I will guide you step by step in this workshop.

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
## Download Forge 1.19
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

## Running Project, Starting Client

Then run *runClient*. You can hit Play after this instead of *runClient*

![Eclipse Gradle Run Client](https://i.imgur.com/FJOVrcn.png)

**Let's make sure we can get minecraft started before continuing.** This is the default example mod we will be replacing

![Minecraft running with Example Mod](https://i.imgur.com/r3OnICr.png)

Let's create a new world as well.

## Introduction

- Developer
- Tinkerer
- Gardener
- Climber
- Cyclist
- Player of modded minecraft

Our mod is based on the kryptonite gem. You can replace that with whatever you'd like and make your own mod.

We'll be using Forge. Forge is a framework for building mods. An alternative would be [Fabric](https://fabricmc.net/) which is lighter weight but seems to have less mods using it.

Pay attention to the version when looking at documentation and other tutorials/blogs. Things change and some info is no longer correct. Try to stick to recent sources that use 1.19 or 1.18.x

## Setting up IDE (IntelliJ)

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
4. Register ITEMS on the eventBus
5. Register ModItems on the modEventBus in **KryptoniteMod.java**
6. Add RegistryObject KRYPTONITE
    - Can add more items by copying this line
    - Many many different properties to use to configure your items. We will come back to this
    - ![So many properties](https://i.imgur.com/KSbzHAf.png)
7. Add KRYPTONITE_INGOT

### Adding asset directories to our Resources
1. Add directories to match this (might be easier to use File Explorer with Ctrl + Shift + N):
    - ![Asset directories](https://i.imgur.com/5mPEyov.png)
2. Add en_us.json in lang folder
    - Add kryptonite_ingot and kryptonite's display names
3. Add kryptonite.json in models > item folder
    - Configure texture
4. Add kryptonite_ingot.json in same folder by copying it (select and hit F5)
5. Add texture files as png's:
    - Use those provided in this repo
    - Can make your own an online editor like [Nova Skin](https://minecraft.novaskin.me/resourcepacks)
    - Or use the External Libraries (Gradle: net.minecraft.client.extra > client-extra.jar > assets > minecraft > textures) and then use Paint, Gimp, etc to edit
        - ![Exteranl Libraries textures](https://i.imgur.com/Aw03Xxc.png)
6. Let's test it out!

At this point your project should look something like branch [3-AddingKryptoniteIngots](https://github.com/TheCodingCanal/KryptoniteMod/tree/3-AddingKryptoniteItems)

## Adding Kryptonite Blocks
### The ModBlocks.java file
1. Add DeferredRegister BLOCKS
2. Register BLOCKS on the event bus
3. Register ModBlocks on the modEventBus in **KryptoniteMod.java**
4. Create registerBlock function. These are helper functions
5. Register block items as well. Blocks are items as well and need to be registered as such
6. Call registerBlockItem method from registerBlock
7. Register Kryptonite Block
    - Many materials to choose from which give it the correct sounds and visuals
    - Strength of 3f (float) sets how long it takes to mine
    - Currently won't drop any items until we configure the loot json files
    - ![Many properties to use](https://i.imgur.com/wZontXY.png)
8. Register kryptonite ores
    - Use DropExperienceBlock instead of regular
    - Will give random amount experience between 3 and 6
    - Feel free to change things up to test out these properties and methods

### Kryptonite block assets
1. Create kryptonite_block.json, kryptonite_ore.json, and deepslate_kryptonite_ore.json in blockstates
    - This defines the different states and variants for your block
    - More info can be found in the [Forge docs](https://docs.minecraftforge.net/en/1.12.x/models/using/#block-models)
2. Create kryptonite_block.json, kryptonite_ore.json, and deepslate_kryptonite_ore.json in models > block
    - Using a cube texture with a single texture file for all sides
3. Create kryptonite_block.json, kryptonite_ore.json, and deepslate_kryptonite_ore.json in models > item
    - refer to block model
4. Add our blocks' display names to en_us.json in lang folder

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