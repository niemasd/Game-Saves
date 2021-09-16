# Cheat Engine Notes

## Total Enemies Killed
This is a 2-byte integer at address `0139C53C`.

## Items
The inventory starts at address `0139F7CC`. Each item in the inventory is represented using 4 bytes:
* Bytes 1-2 = item value (array of byte)
* Byte 3 = item count (unsigned integer)
* Byte 4 = unknown function (usually 0)

### Changing Items
The first inventory item slot is at address `0139F7CC`, and each subsequent item is 4 bytes further (e.g. the second item is at address `139F7D0`). Set the inventory slot's item value to one of the following (these are hex values):

#### Consumables
* Anything less than `9B` seems to crash the game
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

#### Weapons
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
