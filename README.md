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
1. Download or clone this repository to your Atom-TTS directory (by default that's "C:/Documents/Tabletop Simulator").
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

|             | Format                                  | Example                              |
|-------------|-----------------------------------------|--------------------------------------|
| Simple      | `Amount Cardname`                       | `$spawn 1 Luminarch Aspirant`        |
| MTGA        | `Amount Cardname (SetID) CollectorID`   | `$spawn 15 Plains (THB) 250`         |
| MTGO        | `Amount Cardname [SetID]`               | `$spawn The Meathook Massacre [MID]` |
| MTGO(exact) | `Amount Cardname <CollectorID> [SetID]` | `$spawn 3 Swamp <252> [THB]`         |

The MTGA and MTGO(exact) Formats are useful for getting specific prinitngs of a card. Both of the examples shown here get the cool Cosmos-Lands from THB.

#### $token [characteristics]

Attempts to spawn a token with all the given characteristics.

Characteristics include keywords, power/toughness, creature type and color. You can put these in any order.

For example: `$token 1/1 Vampire Lifelink` will spawn a 1/1 Vampire with lifelink. If several token match the charecteristics, it will spawn a random one. For example `Vampire lifelink` can produce 5 different tokens. use as many characteristics as you can.

Since tokens don't have unique identifiers, this does not always work as expected.
My advise is to try this a few times and if it doesn't work, manually get the token from scryfall.
When searching for tokens on scryfall, don't forget to add `is:token` to your query.

###### Special Tokens

There are some special tokens like "Vecna", "Marit Lage" and the tokens created by the Eternalize ability. For thos etokens, please just use the name like this: `$token Vecna`

#### $random [query]

Spawns a random card, that matches the given scryfall query string.
Click [here](https://scryfall.com/docs/syntax) to learn more about scryfall querys.

#### $booster [setID]

Spawns a 14-card draft booster from the given setID. These are made up of 10 commons, 3 uncommons and 1 rare or mythic rare.

Note: Draft boosters usually have 15 cards in them, but I am omitting the single basic land that is in every draft booster.

#### $setSleeve [url]

This sets your current sleeve in the game data to the image at this url. Rightclick a card or deck and select "Sleeve" to apply this sleeve to the card or deck.

Your current sleeve is not stored between sessions.

#### $setScale [scale]

This will set the scale at which cards are spawned. Setting this to 0.5, for example, will spawn cards at half height and width.

This does not affect cards that are already in play, but you can rightclick any card or deck and select "Scale" to apply the current scale.

Scale is global for all players and does not persist through games.

### Context Menu

This script also adds some extra context menu options:

#### Sleeves

Apply your current sleeve to a card or deck.
Use $setSleeve to select a current sleeve first.

#### Scale

Apply the current scale to a card or deck.
Use $setScale to select a scale first.

#### Dual-Faced Cards.

Only appears on modal dual faced cards like the zendikar dual lands.
Flips the card to the other side
