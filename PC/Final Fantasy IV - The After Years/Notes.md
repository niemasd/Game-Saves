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
* Bytes 1-2 = item value
* Byte 3 = item count (unsigned integer)
* Byte 4 = unknown function (usually 0)

### Changing Items
The first inventory item slot is at address `0139F7CC`, and each subsequent item is 4 bytes further (e.g. the second item is at address `139F7D0`). Set the inventory slot's item value to one of the following 2-byte values:

```
D1 07 Flame Claws
D2 07 Ice Claws
D3 07 Lightning Claws
D4 07 Faerie Claws
D5 07 Hell Claws
D6 07 Cat Claw s
D7 07 Rod
D8 07 Ice Rod
D9 07 Flame Rod
DA 07 Thunder Rod
DB 07 Polymorph Rod
DC 07 Faerie Rod
DD 07 Stardust Rod
DE 07 Lilith Rod
DF 07 Staff
E0 07 Healing Staff
E1 07 Mythril Staff
E2 07 Power Staff
E3 07 Aura Staf
E4 07 Sage’s Staff
E5 07 Rune Staff
E6 07 Dark Sword
E7 07 Shadow Blade
E8 07 Deathbringer
E9 07 Mythgraven Blade
EA 07 Lustrous Sword
EB 07 Excalibur
EC 07 Flame Sword
ED 07 Icebrand
EE 07 Defender
EF 07 Blood Sword
F0 07 Ancient Sword
F1 07 Sleep Blade
F2 07 Stoneblade
F3 07 Spear
F4 07 Wind Spear
F5 07 Flame Lance
F6 07 Ice Lance
F7 07 Wyvern Lance
F8 07 Holy Lance
F9 07 Blood Lance
FA 07 Gungnir
FB 07 Kunai
FC 07 Ashura
FD 07 Kotetsu
FE 07 Kiku-Ichimonji
FF 07 Murasame
00 08 Musasame
01 08 Assassin’s Dagger
02 08 Mage Masher
03 08 Thorn Whip
04 08 Chain Whip
05 08 Blitz Whip
06 08 Flame Whip
07 08 Dragon Whisker
08 08 Crescent Axe
09 08 Dwarven Axe
0A 08 Orgekiller
0B 08 Mythril Knife
0C 08 Dancing Dagger
0D 08 Mythril Sword
0E 08 Kitchen Knife
0F 08 Ragnarok
10 08 Shuriken
11 08 Fuma Shuriken
12 08 Boomerang
13 08 Moonring Blade
14 08 Dream Harp
15 08 Lamia Harp
16 08 Blank
17 08 Poison Axe
18 08 Rune Axe
19 08 Mythril Hammer
1A 08 Gaia Hammer
1B 08 Wooden Hammer
1C 08 Avenger
1D 08 Bow
1E 08 Cross Bow
1F 08 Great Bow
20 08 Killer Bow
21 08 Elfin Bow
22 08 Yoichi Bow
23 08 Artemis Bow
24 08 Iron Arrows
25 08 Holy Arrows
26 08 Fire Arrows
27 08 Ice Arrows
28 08 Lightning Arrows
29 08 Dark Arrows
2A 08 Poison Arrows
2B 08 Silencing Arrows
2C 08 Angel Arrows
2D 08 Yoichi Arrows
2E 08 Medusa Arrows
2F 08 Artemis Arrows
30 08 Blank
31 08 Iron Shield
32 08 Dark Shield
33 08 Demon Shield
34 08 Lustrous Shield
35 08 Mythril Shield
36 08 Flame Shield
37 08 Ice Shield
38 08 Diamond Shield
39 08 Aegis Shield
3A 08 Genji Shield
3B 08 Dragon Shield
3C 08 Crystal Shield
3D 08 Iron Helm
3E 08 Dark Helm
3F 08 Hades Helm
40 08 Demon Helm
41 08 Lustrous Helm
42 08 Mythril Helm
43 08 Diamond Helm
44 08 Genji Helm
45 08 Dragon Helm
46 08 Crystal Helm
47 08 Leather Cap
48 08 Feathered Cap
49 08 Wizard’s Hat
4A 08 Sage’s Miter
4B 08 Gold Hairpin
4C 08 Ribbon
4D 08 Headband
4E 08 Green Beret
4F 08 Black Cowl
50 08 Glass Mask
51 08 Iron Armor
52 08 Dark Armor
53 08 Hades Armor
54 08 Demon Armor
55 08 Knight’s Armor
56 08 Mythril Armor
57 08 Flame Mail
58 08 Ice Armor
59 08 Diamond Armor
5A 08 Genji Armor
5B 08 Dragon Mail
5C 08 Crystal Mail
5D 08 Clothing
5E 08 Leather Clothing
5F 08 Gaia Gear
60 08 Sage’s Surplice
61 08 Black Robe
62 08 Luminous Robe
63 08 White Robe
64 08 Power Sash
65 08 Minerva Bustier
66 08 Prison Garb
67 08 Bard’s Tunic
68 08 Kenpo Gi
69 08 Black Belt Gi
6A 08 Adamant Armor
6B 08 Black Garb
6C 08 Iron Gloves
6D 08 Dark Gloves
6E 08 Hades Gloves
6F 08 Demon Gloves
70 08 Gauntlets
71 08 Mythril Gloves
72 08 Diamond Gloves
73 08 Giant’s Gloves
74 08 Genji Gloves
75 08 Dragon Gloves
76 08 Crystal Gloves
77 08 Iron Armet
78 08 Ruby Ring
79 08 Silver Armlet
7A 08 Power Armlet
7B 08 Rune Armlet
7C 08 Crystal Ring
7D 08 Diamond Armlet
7E 08 Protect Ring
7F 08 Cursed Ring
80 08 Bomb Fragment
81 08 Bomb Crank
82 08 Antarctic Wind
83 08 Arctic Wind
84 08 Zeus’s Wrath
85 08 Heavenly Warth
86 08 Stardust
87 08 Lillith’s Kiss
88 08 Vampire Fang
89 08 Bacchus’s Wine
8A 08 Hermes Sandals
8B 08 Bronze Hourglass
8C 08 Silver Hourglass
8D 08 Gold Hourglass
8E 08 Spider Silk
8F 08 Decoy
90 08 Red Fang
91 08 White Fang
92 08 Blue Fang
93 08 Light Curtain
94 08 Bomb Core
95 08 Lunar Curtain
96 08 Silent Bell
97 08 Gaia Drum
98 08 Crystal
99 08 Coeurl Whisker
9A 08 Blank
9B 08 Bestiary
9C 08 Alarm Clock
9D 08 Unicorn Horn
9E 08 Potion
9F 08 Hi-Potion
A0 08 X-Potion
A1 08 Ether
A2 08 Dry Ether
A3 08 Elixir
A4 08 Phoenix Down
A5 08 Gold Needle
A6 08 Maiden’s Kiss
A7 08 Mallet
A8 08 Diet Ration
A9 08 Echo Herbs
AA 08 Eye Drops
AB 08 Antidote
AC 08 Cross
AD 08 Remedy
AE 08 Siren
AF 08 Golden Apple
B0 08 Silver Apple
B1 08 Soma Drop
B2 08 Tent
B3 08 Cottage
B4 08 Lustful Lali-Ho
B5 08 Emergency Exit
B6 08 Gnomish Bread
B7 08 Goblin
B8 08 Bomb
B9 08 Cockatrice
BA 08 Mindflayer
BB 08 Blank
BC 08 Member’s Writ
BD 08 Blank
BE 08 Blank
BF 08 Blank
C0 08 Sand Pearl
C1 08 Blank
C2 08 Blank
C3 08 Blank
C4 08 Blank
C5 08 Blank
C6 08 Blank
C7 08 Adamantite
C8 08 Frying Pan
C9 08 Pink Tail
CA 08 Blank
CB 08 Blank
CC 08 Godhand
CD 08 Apollo’s Harp
CE 08 Triton’s Dagger
CF 08 Serahim’s Mace
D0 08 Thor’s Hammer
D1 08 Lightbringer
D2 08 Index Finger
D3 08 Excalipoor
D4 08 Abel’s Lance
D5 08 Flare Sledgehammer
D6 08 Dragon Gloves
D7 08 Hanzo’s Gloves
D8 08 Martial Armlet
D9 08 White Ring
DA 08 Mist Ring
DB 08 Harmony Ring
DC 08 Blank
DD 08 Blank
DE 08 Blank
DF 08 Blank
E0 08 Blank
E1 08 Blank
E2 08 Blank
E3 08 Blank
E4 08 Blank
E5 08 Blank
E6 08 Brave Suit
E7 08 Red Jacket
E8 08 Sage’s Robe
E9 08 Robe of Lords
EA 08 Grand Armor
EB 08 White Tiger Mask
EC 08 Red Cap
ED 08 Hypnocrown
EE 08 Cat-Ear Hood
EF 08 Grand Helm
F0 08 Nirvana
F1 08 Asura’s Rod
F2 08 Sasuke’s Katana
F3 08 Matsunokami
F4 08 Mystic Whip
F5 08 Perseus’s Bow
F6 08 Perseus Arrows
F7 08 Tiger Fangs
F8 08 Dragon Claws
F9 08 Loki’s Lute
FA 08 Rising Sun
FB 08 Assassin’s Dagger
FC 08 Giant Axe
FD 08 Hog Call
FE 08 Hero’s Shield
FF 08 Rainbow Robe
00 09 White Dress
01 09 Chocobo Suit
02 09 Tabby Suit
03 09 Maximillian
04 09 Caesar’s Plate
05 09 Blank
06 09 Assassin Vest
07 09 Battle Gear
08 09 Vishnu Vest
09 09 Blank
0A 09 Blank
0B 09 Blank
0C 09 Blank
0D 09 Blank
0E 09 Blank
0F 09 Blank
10 09 Blank
11 09 Blank
12 09 Megalixir
13 09 Bloody Spear
14 09 Requiem Harp
15 09 Broadsword
16 09 Longsword
17 09 Iron Sword
18 09 Coral Sword
19 09 Bronze Shield
1A 09 Bronze Helm
1B 09 Steel Helm
1C 09 Bronze Armor
1D 09 Chainmail
1E 09 Plate Mail
1F 09 Javelin
20 09 Trident
21 09 Partisan
22 09 Kingsword
23 09 Falchion
24 09 Training Garb
25 09 Large Shield
26 09 Turban
27 09 Blue Tail
28 09 Flan Ring
29 09 Sprint Ring
2A 09 Hammer
2B 09 Boy’s Clothes
2C 09 Girl’s Clothes
2D 09 Knife
2E 09 Dagger
2F 09 Warrior’s Clothes
30 09 Clown’s Clothes
31 09 Mage’s Clothes
32 09 Angel’s Clothes
33 09 Circlet
34 09 Mage’s Robe
35 09 Battle Axe
36 09 Horned Armor
37 09 Horned Helmet
38 09 Tomahawk
39 09 Kokkol Ore
3A 09 Whip
3B 09 Healing Rod
3C 09 Green Tail
3D 09 Agartite
3E 09 Mythril Spring
3F 09 Mythril Bolt
40 09 Mythril Nut
41 09 Bronze Breastplate
42 09 Silver Breastplate
43 09 Hyper Wrist
44 09 Rose Twine Dress
45 09 Metal Knuckles
46 09 Kaiser Knuckles
47 09 Red Tail
48 09 Chakra Band
49 09 Foot Ninja Gear
4A 09 Shinobi Gear
4B 09 Black Tail
4C 09 Psycho Spiral
4D 09 Member’s Card
4E 09 VIP Card
4F 09 Wizard’s Rod
50 09 Queen’s Whip
51 09 Queen’s Tights
52 09 Queen’s Mask
53 09 Queen’s Gloves
54 09 Protect Staff
55 09 Mystic Veil
56 09 Talisman
57 09 Red Robe
58 09 Single Star
59 09 Kodachi
5A 09 Metal Boomerang
5B 09 Manji Shuriken
5C 09 Kogarasu
5D 09 Stell Headplate
5E 09 Purple Tail
5F 09 Chakram
60 09 Goblin Mask
61 09 Mist Wrap
62 09 Treasure Hunter
63 09 Crimson Cherry
64 09 Wing Edge
65 09 Rapid Ring
66 09 Ring of Memories
67 09 Amulet of Memories
68 09 White Tail
69 09 Whisperweed Seed
6A 09 Poet’s Notebook
6B 09 Bard’s Lyre
6C 09 Gil Bird Egg
6D 09 Silver Harp
6E 09 Blank
6F 09 Blank
70 09 Blank
71 09 Blank
72 09 Blank
73 09 Gil Band
74 09 Economical Ring
75 09 Damcyan Flowers
76 09 Velour Coat
77 09 Dark Harp
78 09 Beret
79 09 Gold Tail
7A 09 Silver Tail
7B 09 Muse Harp
7C 09 Officer’s Hat
7D 09 Ice Whip
7E 09 Level Band
7F 09 Bronze Tail
80 09 Exorcist’s Gown
81 09 Professor’s Rope
82 09 Dragon Lance
83 09 Cross Helm
84 09 Bone Wrist
85 09 Gray Tail 
86 09 Demon Slayer
87 09 Obelisk
88 09 Sledgehammer
89 09 Ebony Robe
8A 09 Eboy Blade
8B 09 Ebony Tail
8C 09 Rare Band
8D 09 Master’s Staff
8E 09 Proof of Courage
8F 09 Enhancement Sword
90 09 Ladle
91 09 Ramuh Staff
92 09 Shiva Crystal
93 09 Sylph Feather
94 09 Chocobo
95 09 Blank
96 09 Blank
97 09 Boltslicer
98 09 Bone Mail
99 09 Small Tail
9A 09 Blank
9B 09 Small Tale
9C 09 Blank
9D 09 Rainbow Tail
9E 09 Recovery Rod
9F 09 Blank
A0 09 Fire Scarf
A1 09 Ultima Weapon
A2 09 Adamant Shield
A3 09 Adamant Helm
A4 09 Adamant Gloves
A5 09 Pink Armor
A6 09 Twin Stars
A7 09 Treasure Hunter v2
A8 09 Rapid Ring v2
A9 09 Gil Band v2
AA 09 Level Band v2
AB 09 Rare Band v2
AC 09 Limit Ring 
AD 09 Reach Ring
AE 09 Taunt Ring
AF 09 Tokita Sword
B0 09 Akiyama Armor
B1 09 Final Outfit
B2 09 Blue Armor
B3 09 Discovery Book
B4 09 Crystal
B5 09 Lunar Shield
B6 09 Lunar Helm
B7 09 Lunar Mail
B8 09 Lunar Gloves
B9 09 Phase Cutter
BA 09 Phase Body
BB 09 Phase Helm
BC 09 Phase Knuckles
BD 09 Phase Shield
```
