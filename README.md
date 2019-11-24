# Introduction
The M3C (Minecraft ComputerCraft) repository is a (somewhat) simple collection of Lua scripts written for [ComputerCraft 1.75](http://www.computercraft.info/2015/12/04/computercraft-1-75/) in Minecraft 1.7.10. These scripts may or may not be compatible with other versions of ComputerCraft.

As our primary purpose for creating these scripts was to monitor specific things around our base, most of these scripts are of the useful genre. However, some of these scripts are completely for fun like the "cowsay" and "changeLights" scripts. Nearly all of these scripts are designed to work in conjunction with each other as you will see below.

# Contributions
We would love for anyone to PR any additional scripts or modifications to our existing scripts! While we aren't actively playing Minecraft at the moment, that doesn't mean we have lost interest in the scripting side of ComputerCraft. :) All we ask is that your scripts make sense and follow the very general/informal convention of our other scripts.

# How To Begin
1. Open the computer that you wish to run our scripts on.
2. Name the computer for posterity by typing the following: `label set labelName` where `labelName` is the name you wish to apply to the computer.
3. Type `edit startup`
4. Place the below contents into this script.
```
shell.run("delete github*")
shell.run("pastebin run p8PJVxC4")
shell.run('github clone "Joshua-Brent-Collins/M3C"')
term.clear()
term.setCursorPos(1,1)
```
5. Save and close the startup file.
6. Hold Ctrl + R to reboot the computer to test the startup script. You should see some terminal output briefly before it clears.
7. Type `ls` to view the contents of the base directory. You should see a folder named "M3C". You're now ready to begin!

# Scripts
## changeLights
* A script of the "fun" persuasion. This script will utilize a [Sensor](https://ftbwiki.org/Sensor) from the [Open Peripheral](https://ftbwiki.org/OpenPeripheral) mod to detect when players enter the proximity of the sensor. Upon doing so, it will change the color of one or more [Glowstone Illuminators](https://ftbwiki.org/Glowstone_Illuminator) automatically to match the player's preferred color.
* The sensor can be attached directly, but the Glowstone Illuminators would be best hooked up via [Networking Cable](http://www.computercraft.info/wiki/Networking_Cable) and [Wired Modems](http://www.computercraft.info/wiki/Wired_Modem).
* Modify the `playerPreferences` table to include the Minecraft player names of those you wish to set a color preference for. The value in that table should be a Hex code to match the color. Ex: Red = 0xFF0000.
* When no players are detected within the range of the Sensor, the lights will set to black to imitate the lights being turned off.
* When multiple players are within the range of the sensor, the lights will alternate through all detected players' preferences in one second intervals.

## cowsay
* Every 5 minutes, fetch a random Chuck Norris joke from [The Internet Chuck Norris Database](http://www.icndb.com/). Take that joke, and then send it through [Cowsay](http://cowsay.morecode.org/) to print the ASCII of a cow saying the Chuck Norris joke on a group of monitors.
* Requires at least a 5 block wide x 3 block high [Advanced Monitor](https://ftbwiki.org/Advanced_Monitor) setup. The monitors must be connected directly to the back of the computer running this script.
* Requires [this JSON ComputerCraft API](http://www.computercraft.info/forums2/index.php?/topic/5854-json-api-v201-for-computercraft/) named as `json` and placed in a `scripts/` folder.

## glassesHud
* Requires use of a [Terminal Glasses Bridge](https://ftbwiki.org/Terminal_Glasses_Bridge) and [Terminal Glasses](https://ftbwiki.org/Terminal_Glasses).
* This script reads values from the K/V server and prints them out onto the HUD of any player with Terminal Glasses that have been connected to the Terminal Glasses Bridge used by the script.
* Prints a semi-transparent box in the upper-left hand corner with one stat from the K/V server per line.
* Starts with a 20-pixel buffer from the top for players who use [jetpacks](https://ftb.gamepedia.com/Jetpack_(Simply_Jetpacks)) from the Simply Jetpacks mod.

## kv
* A very lightweight script designed to be the server in the K/V server.
* Started up using `kv server restore`. If you don't wish to restore your K/V pairs from the backed up floppy disk, you can simply use `kv server` instead.

## kvApi
* Houses the real meat of the K/V server system.
* Contains all methods needed to fully utilize the K/V server. Primary methods are `clientGet()`, `clientStore()`, and `deserializeKvResponse()`.

## meMonitor
* Requires a K/V server setup.
* Every 30 seconds, read the drive data from a [ME Network](https://ftbwiki.org/ME_Network) and send that data to the K/V server. Also sends the `os.time()` to represent when the data was last gathered.
* [ME Drives](https://ftbwiki.org/ME_Drive) should be connected to the computer via Networking Cable and Wired Modems.
* Data gathered:
    * Storage Cell Slots (Available, Used, Total)
    * Storage Cell Bytes (Available, Used, Total)

## powerStation
* Requires a K/V server setup.
* Every 30 seconds, read the power data from a series of [Thermal Expansion Energy Cells](https://ftbwiki.org/Resonant_Energy_Cell) and send that data to the K/V server. Also sends the `os.time()` to represent when the data was last gathered.
* Data gathered:
    * Stored energy
    * Total energy capacity
    * Percentage of capacity stored

## reactorFuel
* Requires a K/V server setup.
* Every 30 seconds, read the contents of one or more [Deep Storage Units](https://ftbwiki.org/Deep_Storage_Unit) and send that data to the K/V server. Also sends the `os.time()` to represent when the data was last gathered.
* We used this exclusively for monitoring our [Yellorium](https://ftbwiki.org/Yellorium_Ingot) and [Blutonium](https://ftbwiki.org/Blutonium_Ingot) reserves for our [Big Reactor](https://ftbwiki.org/Big_Reactors), but by changing what key is sent to the K/V server, you can monitor anything you'd like.

## rsController
* A fairly simple yet robust redstone signal controller.
* Arguments:
    * Side to output signal on
    * How long the first series lasts.
    * How long the second series lasts.
    * Whether to start the signal as on or off.
    * (Optional) Verbose mode for logging the status.
* We used this to initially help regulate our [Mass Fabricator](https://ftbwiki.org/Mass_Fabricator) from using too much power early in the game. We wound up using a more specific script later on that balanced power usage with [scrap](https://ftbwiki.org/Scrap) consumption.

## sesame
* One of our sillier scripts. This script utilizes a Sensor (similar to changeLights above) to detect when a player has approached. Upon doing so, a door chime is played using a [Note Block](https://minecraft.gamepedia.com/Note_Block) and a redstone signal is sent out on both sides. Our redstone signal is sent to two sticky pistons for a vanilla-like automation of a door. After exiting the Sensor range, the opposite door chime plays and the redstone signal stops.

## utils
* Simply a utility library. It provides the following utilities:
    * `drawBargraph` - Drawing a bargraph on a monitor.
    * `findAndWrap` - Find a peripheral on an arbitrary side of the computer based on its type. Returns that wrapped peripheral.
        * Supports a peripheral that is connected via a Wired Modem.
    * `findAndWrapAll` - Find all peripherals on any arbitrary side of the computer based on the peripheral's type. Returns a table of the wrapped peripherals.
        * This supports any peripherals that are connected via a Wired Modem.
        * Specify second argument as `true` if the argument you're passing should match peripheral names based on a "starts with" criteria.
    * `orderTable` - Used in conjunction with a `for` loop to iterate through a table that is sorted in alpha order based on the keys of the table.
    * `printTable` - A simple script to iterate through a table and print it out to the active terminal screen.
    * `formatInt` - Formats an integer to have comma separators. If the argument cannot be cast as a numeric, returns `-1`.
    * `round` - Rounds a number to a specific number of decimal places.
    * `rednetLookupWithRetry` - Fixes a semi-common bug of a Rednet lookup failing. Attempts a finite amount of times to look up a specified protocol and host on Rednet before giving up and returning `nil`.