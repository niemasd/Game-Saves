# Cheat Engine Notes

## Total Enemies Killed
This is a 2-byte integer at address `0139C53C`.

## Bestiary
The bestiary is represented as kill counts (2-byte unsigned integer) for each monster, with the count seemingly being separate in each Tale. Instead of kill counts incrementing by 1 (`01` in hex), they actually increment by 16 (`10` in hex). Here's the mapping of decimal true kill count to hex bestiary kill count:

```
Slays	Data
0(Seen)	0100
1	1100
2	2100
3	3100
4	4100
5	5100
6	6100
7	7100
8	8100
9	9100
10	A100
11	B100
12	C100
13	D100
14	E100
15	F100
16	0101
17	1101
18	2101
19	3101
20	4101
21	5101
22	6101
23	7101
24	8101
25	9101
26	A101
27	B101
28	C101
29	D101
30	E101
31	F101
32	0102
33	1102
34	2102
35	3102
36	4102
37	5102
38	6102
39	7102
40	8102
41	9102
42	A102
43	B102
44	C102
45	D102
46	E102
47	F102
48	0103
49	1103
50	2103
51	3103
52	4103
53	5103
54	6103
55	7103
56	8103
57	9103
58	A103
59	B103
60	C103
61	D103
62	E103
63	F103
64	0104
65	1104
66	2104
67	3104
68	4104
69	5104
70	6104
71	7104
72	8104
73	9104
74	A104
75	B104
76	C104
77	D104
78	E104
79	F104
80	0105
81	1105
82	2105
83	3105
84	4105
85	5105
86	6105
87	7105
88	8105
89	9105
90	A105
91	B105
92	C105
93	D105
94	E105
95	F105
96	0106
97	1106
98	2106
99	3106
100	4106
101	5106
102	6106
103	7106
104	8106
105	9106
106	A106
107	B106
108	C106
109	D106
110	E106
111	F106
112	0107
113	1107
114	2107
115	3107
116	4107
117	5107
118	6107
119	7107
120	8107
121	9107
122	A107
123	B107
124	C107
125	D107
126	E107
127	F107
128	0108
129	1108
130	2108
131	3108
132	4108
133	5108
134	6108
135	7108
136	8108
137	9108
138	A108
139	B108
140	C108
141	D108
142	E108
143	F108
144	0109
145	1109
146	2109
147	3109
148	4109
149	5109
150	6109
151	7109
152	8109
153	9109
154	A109
155	B109
156	C109
157	D109
158	E109
159	F109
160	010A
161	110A
162	210A
163	310A
164	410A
165	510A
166	610A
167	710A
168	810A
169	910A
170	A10A
171	B10A
172	C10A
173	D10A
174	E10A
175	F10A
176	010B
177	110B
178	210B
179	310B
180	410B
181	510B
182	610B
183	710B
184	810B
185	910B
186	A10B
187	B10B
188	C10B
189	D10B
190	E10B
191	F10B
192	010C
193	110C
194	210C
195	310C
196	410C
197	510C
198	610C
199	710C
200	810C
201	910C
202	A10C
203	B10C
204	C10C
205	D10C
206	E10C
207	F10C
208	010D
209	110D
210	210D
211	310D
212	410D
213	510D
214	610D
215	710D
216	810D
217	910D
218	A10D
219	B10D
220	C10D
221	D10D
222	E10D
223	F10D
224	010E
225	110E
226	210E
227	310E
228	410E
229	510E
230	610E
231	710E
232	810E
233	910E
234	A10E
235	B10E
236	C10E
237	D10E
238	E10E
239	F10E
240	010F
241	110F
242	210F
243	310F
244	410F
245	510F
246	610F
247	710F
248	810F
249	910F
250	A10F
251	B10F
252	C10F
253	D10F
254	E10F
255	F10F
```

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
