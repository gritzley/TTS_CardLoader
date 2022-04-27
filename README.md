# MTG Card Loader for TTS
This is a library for Tabletop Simulator that allows you to load MTG cards and adds some
additional utility to Cards.

## Setup

There are two ways to set up this project.

One uses the Atom TTS Plugin, which basically compiles a whole list of files into the TTS savegame, which usually can't handle multiple files.

The other is to just dump the code that I copy/pasted from the built version of the previous method into the game.

### Method 1: Do it properly

#### Prerequisites

- [Tabletop Simulator](https://store.steampowered.com/app/286160/Tabletop_Simulator/)
- [Atom Text Editor](https://atom.io/)
- [TTS Plugin for Atom](https://atom.io/packages/atom-tts)

#### Installation
1. Download or clone this Repository to "C:/Documents/Tabletop Simulator.
2. Open Tabletop Simulator and create a new game.
3. Select "Modding" in the top bar and in the text editor that opens, write `#include CardLoader/main`
4. Click "Save & Play"

### Method 2: Fuck it, i just want the code

#### Prerequisites

- [Tabletop Simulator](https://store.steampowered.com/app/286160/Tabletop_Simulator/)

#### Installation
1. Open "compiled.ttslua" and copy its contents
2. Open Tabletop Simulator and create a new game.
3. Select "Modding" in the top bar and paste the code into the editor that opens.
4. Click "Save & Play"

## How to use

This library adds some console commands that you can execute by just typing them into the chat and some extra functionality to the context menus of card and deck objects.

### Console commands

#### $import

Open a window in which you can paste a decklist in the MTGA or MTGO Format.
You can download decklists from many popular sites such as [mtggoldfish](https://www.mtggoldfish.com/) and most Programs related to MTG (like MTG Arena) will let you export your decks in one of these two formats.

All cards are spawned at the center of the table.
Currently, there is only one import window for all players so typing this command while another player is using this window will take it away from them. This will be fixed in a future update.

#### $spawn [cardsstring]

Spawn a single card as defined in the cardstring. This cardstring must adhere to one of these formats:

- Simple: **Amount Cardname** *e.G. $spawn 1 Luminarch Aspirant*
- MTGA: **Amount Cardname (SetID) CollectorID** *e.G. $spawn 15 Plains (THB) 250*
- MTGO: **Amount Cardname [SetID]** *e.G. $spawn The Meathook Massacre [MID]*
- MTGO(exact): **Amount Cardname <CollectorID> [SetID]** *e.G. $spawn 3 Swamp <252> [THB]*

The MTGA and MTGO(exact) Formats are useful for getting specific prinitngs of a card. Both of the examples shown here get the cool Cosmos-Lands from THB.

#### $random [query]

Spawns a random card, that matches the given scryfall query string.
Click [here](https://scryfall.com/docs/syntax) to learn more about scryfall querys.

#### $booster [setID]

Spawns a 14-card draft booster from the given setID. These are made up of 10 commons, 3 uncommons and 1 rare or mythic rare.

Note: Draft boosters usually have 15 cards in them, but I am omitting the single basic land that is in every draft booster.

#### $setSleeve [url]

This sets your current sleeve in the game data to the image at this url. Rightclick a card or deck and select "Sleeve" to apply this sleeve to the card or deck.

Your current sleeve is not stored between sessions.

### Other Functionalities

Beyond the console commands, this library adds some other functionalities to cards and decks in TTS.

#### Sleeves

You can rightclick cards and decks and select "Sleeve" to apply your current sleeve to them.
Use $setSleeve to select a current sleeve first.

#### Dual-Faced Cards.

Dual faced cards will appear with a normal card back. Press R while hovering over a dual-faced card to switch its face.
