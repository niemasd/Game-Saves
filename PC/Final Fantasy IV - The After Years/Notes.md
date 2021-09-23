# Cheat Engine Notes

## Total Enemies Killed
This is a 2-byte integer at address `0139C53C`.

## Bestiary

### Individual Per-Tale Bestiary Entries
Each individual per-Tale bestiary entry is represented as 2 bytes in the following format (depicted here as big-endian):

```
NNNNNNNN NNNNDCBA
```
 
* The 12 most-significant bits (`N`s) represent the number of slain monsters as a 12-bit unsigned integer
  * In other words, if this entry is loaded as a 2-byte integer `X`, the number of slain monsters would be `(X >> 4) & 0xFFF`
* The 4 least-significant bits (`DCBA`) represent flags about the entry:
  * `A` represents whether or not the monster has been seen (`1` = seen, `0` = unseen)
  * `B` represents whether or not the monster is "NEW", aka the bestiary entry hasn't been viewed by the player (`1` = "NEW", `0` = not "NEW")
    * If the monster is unseen, "NEW" should be false (aka `BA == 10` shouldn't happen)
  * `C` and `D` seem to be unused (seem to always be `0`)

In my description above, I used a big-endian representation for ease of interpretation, but the 2-byte individual per-Tale bestiary entries are actually stored in memory as little-endian:

```
NNNNDCBA NNNNNNNN
```

I believe this is also how individual bestiary entries are represented in the Final Fantasy IV 3D Remake.

### Individual Global Bestiary Entries
Each individual global bestiary entry is represented as an array of 10 per-Tale bestiary entries = 20 bytes total, one for each of the Tales. The order is exactly the order of the 10 Tales:

1. Ceodore's Tale
2. Rydia's Tale
3. Yang's Tale
4. Palom's Tale
5. Edge's Tale
6. Porom's Tale
7. Edward's Tale
8. Kain's Tale
9. Lunarian's Tale
10. The Crystals

If a monster never shows up in a Tale, the corresponding 2-byte per-Tale entry should be all `0`s. I tried manually changing some such entries to non-zero slain counts, but nothing happened.

### Global Bestiary Table
The global bestiary is represented as an array of 20-byte global bestiary entries (as described above). Some monsters appear multiple times (I think there are multiple versions of certain monsters, perhaps with different stats), but what's confusing is that the monster numbering in the per-Tale bestiary entries in the game aren't consistent. Thus, in my own note-taking, I'm just numbering all instances of a given monster in increasing order of memory address in the global bestiary table.

The order is somewhat related to the PSP bestiary (especially local groups of monsters):

https://finalfantasy.fandom.com/wiki/Bestiary_(The_After_Years)#Enemies_1.E2.80.9325

However, the PC version deviates somewhat significantly from this overall (i.e., the PSP bestiary is a useful tool for reverse-engineering the PC bestiary for exploring local neighbors in the table, but it's not overall very similar). I am working on a global bestiary, and I will add it to this repo when it's finished.

## Items
The inventory starts at address `0139F7CC`. Each item in the inventory is represented using 4 bytes:
* Bytes 1-2 = item value (array of byte)
* Byte 3 = item count (unsigned integer)
* Byte 4 = unknown function (usually 0)

### Changing Items
The first inventory item slot is at address `0139F7CC`, and each subsequent item is 4 bytes further (e.g. the second item is at address `139F7D0`). Set the inventory slot's item value to one of the following (these are hex values):

#### Byte 2 = `07`
* Anything less than `D0` seems to crash the game
* `D0 07` = Empty Name
* `D1 07` = Flame Claws
* `D2 07` = Ice Claws
* `D3 07` = Lightning Claws
* `D4 07` = Faerie Claws
* `D5 07` = Hell Claws
* `D6 07` = Cat Claws
* `D7 07` = Rod
* `D8 07` = Ice Rod
* `D9 07` = Flame Rod
* `DA 07` = Thunder Rod
* `DB 07` = Polymorph Rod
* `DC 07` = Faerie Rod
* `DD 07` = Stardust Rod
* `DE 07` = Lilith Rod
* `DF 07` = Staff
* `E0 07` = Healing Staff
* `E1 07` = Mythril Staff
* `E2 07` = Power Staff
* `E3 07` = Aura Staff
* `E4 07` = Sage's Staff
* `E5 07` = Rune Staff
* `E6 07` = Dark Sword
* `E7 07` = Shadow Blade
* `E8 07` = Deathbringer
* `E9 07` = Mythgraven Blade
* `EA 07` = Lustrous Sword
* `EB 07` = Excalibur
* `EC 07` = Flame Sword
* `ED 07` = Icebrand
* `EE 07` = Defender
* `EF 07` = Blood Sword
* `F0 07` = Ancient Sword
* `F1 07` = Sleep Blade
* `F2 07` = Stoneblade
* `F3 07` = Spear
* `F4 07` = Wind Spear
* `F5 07` = Flame Lance
* Anything greater than `F5` seems to carsh the game

#### Byte 2 = `08`
* `00 08` = Masamune
* `01 08` = Assassin's Dagger
* `02 08` = Mage Masher
* `03 08` = Thorn Whip
* `04 08` = Chain Whip
* `05 08` = Blitz Whip
* `06 08` = Flame Whip
* `07 08` = Dragon Whisker
* `08 08` = Crescent Axe
* `09 08` = Dwarven Axe
* `0A 08` = Ogrekiller
* `0B 08` = Mythril Knife
* `0C 08` = Dancing Dagger
* `0D 08` = Mythril Sword
* `0E 08` = Kitchen Knife
* `0F 08` = Ragnarok
* `10 08` = Shuriken
* `11 08` = Fuma Shuriken
* `12 08` = Boomerang
* `13 08` = Moonring Blade
* `14 08` = Dream Harp
* `15 08` = Lamia Harp
* Anything greater than `16 08` seems to crash the game
* Anything less than `31 08` seems to crash the game
* `31 08` = Iron Shield
* `32 08` = Dark Shield
* `33 08` = Demon Shield
* `34 08` = Lustrous Shield
* `35 08` = Mythril Shield
* `36 08` = Flame Shield
* `37 08` = Ice Shield
* `38 08` = Diamond Shield
* `39 08` = Aegis Shield
* `3A 08` = Genji Shield
* `3B 08` = Dragon Shield
* `3C 08` = Crystal Shield
* `3D 08` = Iron Helm
* `3E 08` = Dark Helm
* `3F 08` = Hades Helm
* `40 08` = Demon Helm
* `41 08` = Lustrous Helm
* `42 08` = Mythril Helm
* `43 08` = Diamond Helm
* `44 08` = Genji Helm
* `45 08` = Dragon Helm
* `46 08` = Crystal Helm
* `47 08` = Leather Cap
* `48 08` = Feathered Cap
* `49 08` = Wizard's Hat
* `4A 08` = Sage's Miter
* `4B 08` = Gold Hairpin
* `4C 08` = Ribbon
* `4D 08` = Headband
* `4E 08` = Green Beret
* `4F 08` = Black Cowl
* `50 08` = Glass Mask
* `51 08` = Iron Armor
* `52 08` = Dark Armor
* `53 08` = Hades Armor
* `54 08` = Demon Armor
* `55 08` = Knight's Armor
* `56 08` = Mythril Armor
* `57 08` = Flame Mail
* `58 08` = Ice Armor
* `59 08` = Diamond Armor
* `5A 08` = Genji Armor
* `5B 08` = Dragon Mail
* `5C 08` = Crystal Mail
* `5D 08` = Clothing
* `5E 08` = Leather Clothing
* `5F 08` = Gaia Gear
* `60 08` = Sage's Surplice
* `61 08` = Black Robe
* `62 08` = Luminous Robe
* `63 08` = White Robe
* `64 08` = Power Sash
* `65 08` = Minerva Bustier
* `66 08` = Prison Garb
* `67 08` = Bard's Tunic
* `68 08` = Kenpo Gai
* `69 08` = Black Belt Gi
* `6A 08` = Adamant Armor
* `6B 08` = Black Garb
* `6C 08` = Iron Gloves
* `6D 08` = Dark Gloves
* `6E 08` = Hades Gloves
* `6F 08` = Demon Gloves
* `70 08` = Gauntlets
* `71 08` = Mythril Gloves
* `72 08` = Diamond Gloves
* `73 08` = Giant's Gloves
* `74 08` = Genji Gloves
* `75 08` = Dragon Gloves
* `76 08` = Crystal Gloves
* `77 08` = Iron Armlet
* `78 08` = Ruby Ring
* `79 08` = Silver Armlet
* `7A 08` = Power Armlet
* `7B 08` = Rune Armlet
* `7C 08` = Crystal Ring
* `7D 08` = Diamond Armlet
* `7E 08` = Protect Ring
* `7F 08` = Cursed Ring
* `80 08` = Bomb Fragment
* `81 08` = Bomb Crank
* `82 08` = Antarctic Wind
* `83 08` = Arctic Wind
* `84 08` = Zeus's Wrath
* `85 08` = Heavenly Wrath
* `86 08` = Stardust
* `87 08` = Lilith's Kiss
* `88 08` = Vampire Fang
* `89 08` = Bacchus's Wine
* `8A 08` = Hermes Sandals
* `8B 08` = Bronze Hourglass
* `8C 08` = Silver Hourglass
* `8D 08` = Gold Hourglass
* `8E 08` = Spider Silk
* `8F 08` = Decoy
* `90 08` = Red Fang
* `91 08` = White Fang
* `92 08` = Blue Fang
* `93 08` = Light Curtain
* `94 08` = Bomb Core
* `95 08` = Lunar Curtain
* `96 08` = Silent Bell
* `97 08` = Gaia Drum
* `98 08` = Crystal
* `99 08` = Coeurl Whisker
* `9A 08` = **CRASHES!!!**
* `9B 08` = Bestiary
* `9C 08` = Alarm Clock
* `9D 08` = Unicorn Horn
* `9E 08` = Potion
* `9F 08` = Hi-Potion
* `A0 08` = X-Potion
* `A1 08` = Ether
* `A2 08` = Dry Ether
* `A3 08` = Elixir
* `A4 08` = Phoenix Down
* `A5 08` = Gold Needle
* `A6 08` = Maiden's Kiss
* `A7 08` = Mallet
* `A8 08` = Diet Ration
* `A9 08` = Echo Herbs
* `AA 08` = Eye Drops
* `AB 08` = Antidote
* `AC 08` = Cross
* `AD 08` = Remedy
* `AE 08` = Siren
* `AF 08` = Golden Apple
* `B0 08` = Silver Apple
* `B1 08` = Soma Drop
* `B2 08` = Tent
* `B3 08` = Cottage
* `B4 08` = Lustful Lali-Ho
* `B5 08` = Emergency Exit
* `B6 08` = Gnomish Bread
* `B7 08` = Goblin
* `B8 08` = Bomb
* `B9 08` = Cockatrice
* `BA 08` = Mindflayer
* Anything greater than `BA` seems to carsh the game
* Anything less than ??? seems to crash the game
* `F5 08` = Perseus's Bow
* `F6 08` = Perseus Arrows
* `F7 08` = Tiger Fangs
* `F8 08` = Dragon Claws
* `F9 08` = Loki's Lute
* `FA 08` = Rising Sun
* `FB 08` = Assassin's Dagger
* `FC 08` = Gigant Axe
* `FD 08` = Hog Call
* `FE 08` = Hero's Shield
* `FF 08` = Rainbow Robe
