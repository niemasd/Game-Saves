# Cheat Engine Notes

## Total Enemies Killed
This is a 2-byte integer at address `0139C53C`.

## Items
The inventory starts at address `0139F7CC`. Each item in the inventory is represented using 4 bytes:
* Byte 1 is an integer representing what item it is
* Byte 2 is an integer with some unknown function
* Byte 3 is an integer representing the count of the item
* Byte 4 is an integer with some unknown function (usually 0)

### Changing Items
The first inventory item slot is at address `0139F7CC`, and each subsequent item is 4 bytes further (e.g. the second item is at address `139F7D0`). Set the inventory slot's item value to one of the following (these are decial values)
* `158` = Potion
* `159` = Hi-Potion
* `160` = X-Potion
* `161` = Ether
* `162` = Dry Ether
* `163` = Elixir
* `164` = Phoenix Down
* `165` = Gold Needle
* `166` = Maiden's Kiss
* `167` = Mallet
* `168` = Diet Ration
* `169` = Echo Herbs
* `170` = Eye Drops
* `171` = Antidote
* `172` = Cross
* `173` = Remedy
* `174` = Siren
* `175` = Golden Apple
* `176` = Silver Apple
* `177` = Soma Drop
* `178` = Tent
* `179` = Cottage
* `180` = Lustful Lali-Ho
* `181` = Emergency Exit
* `182` = Gnomish Bread
* `183` = Goblin
* `184` = Bomb
* `185` = Cockatrice
* `186` = Mindflayer
* Anything larger than 186 crashes the game
