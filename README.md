# lua-cairn
A collection of LUA scripts and Redis commands that automate the generation of a Cairn RPG character ( https://cairnrpg.com/ )  and roll virtual dice

The examples and functonality are details below:

## My overarching intent is that this set of scripts makes the generation of NPCs and new characters super quick - the ongoing game play and such would reside in the realm of pencil and paper.


### DATA LOAD SCRIPT -- loads the variable values normally used in the first edition of Cairn https://cairnrpg.com/  these values are then used by LUA scripts to generate characters and roll dice.

### Note that for simplicity and with the knowledge that this does not involve a large amount of data, two arguments are passed to the script:
1. the numver of unique redis key names the LUA engine should be aware of (this allows for the Redis LUA engine to anticipate if any cross-slot errors may occurr)
2. the value to be used as the routing value, or slot-assignment value for any and all keys built using this script  ( below I use the value {cairn} )

```
EVAL "redis.call('SADD', '{cairn}d4', '1','2','3','4') redis.call('SADD', '{cairn}d6', '1','2','3','4','5','6') redis.call('SADD', '{cairn}d8', '1','2','3','4','5','6','7','8') redis.call('SADD', '{cairn}d10', '1','2','3','4','5','6','7','8','9','10') redis.call('SADD', '{cairn}d12', '1','2','3','4','5','6','7','8','9','10','11','12') redis.call('SADD', '{cairn}d20','1','2','3','4','5','6','7','8','9','10','11','12','13','14','15','16','17','18','19','20') redis.call('SADD', '{cairn}d100', '1','2','3','4','5','6','7','8','9','10','11','12','13','14','15','16','17','18','19','20','21','22','23','24','25','26','27','28','29','30','31','32','33','34','35','36','37','38','39','40','41','42','43','44','45','46','47','48','49','50','51','52','53','54','55','56','57','58','59','60','61','62','63','64','65','66','67','68','69','70','71','72','73','74','75','76','77','78','79','80','81','82','83','84','85','86','87','88','89','90','91','92','93','94','95','96','97','98','99','100') redis.call('SADD', '{cairn}ffnames', 'Agune','Beatrice','Breagan','Bronwyn','Cannora','Drelil','Elgile','Esme','Groua','Henaine','Lirann','Lirathil','Lisabeth','Moralil','Morgwen','Sybil','Theune','Wenlan','Ygwal','Yslen') redis.call('SADD', '{cairn}lnames', 'Abernathy','Addercap','Burl','Candlewick','Cormick','Crumwaller','Dunswallow','Getri','Glass','Harkness','Harper','Loomer','Malksmilk','Smythe','Sunderman','Swinney','Thatcher','Tolmen','Weaver','Wolder') redis.call('SADD', '{cairn}mfnames', 'Arwel','Bevan','Boroth','Borrid','Breagle','Breglor','Canhoreal','Emrys','Ethex','Gringle','Grinwit','Gruwid','Gruwth','Gwestin','Mannog','Melnax','Orthax','Triunein','Wenlan','Yirmeor') redis.call('SADD', '{cairn}backgrounds', 'Alchemist','Blacksmith','Butcher','Burglar','Carpenter','Cleric','Gambler','Gravedigger','Herbalist','Hunter','Magician','Mercenary','Merchant','Miner','Outlaw','Performer','Pickpocket','Smuggler','Servant','Ranger') redis.call('SADD', '{cairn}physique', 'Athletic','Brawny','Flabby','Lanky','Rugged','Scrawny','Short','Statuesque','Stout','Towering') redis.call('SADD', '{cairn}skin', 'Birthmark','Dark','Freckled','Pockmarked','Rosy','Pale','Soft','Tanned','Tatooed','Weathered') redis.call('SADD', '{cairn}hair', 'Bald','Braided','Curly','Filthy','Frizzy','Long','Luxurious','Oily','Wavy','Wispy') redis.call('SADD', '{cairn}face', 'Bony','Broken','Chiseled','Elongated','Round','Lovely','Rat-like','Sharp','Square','Sunken') redis.call('SADD', '{cairn}speech', 'Blunt','Booming','Cryptic','Droning','Formal','Gravelly','Precise','Squeaky','Stuttering','Whispery') redis.call('SADD', '{cairn}clothing', 'Antique','Bloody','Elegant','Filthy','Foreign','Frayed','Frumpy','Livery','Rancid','Soiled') redis.call('SADD', '{cairn}virtue', 'Ambitious','Cautious','Courageous','Disciplined','Gregarious','Honorable','Humble','Merciful','Serene','Tolerant') redis.call('SADD', '{cairn}vice', 'Aggressive','Bitter','Craven','Deceitful','Greedy','Lazy','Nervous','Rude','Vain','Vengeful') redis.call('SADD', '{cairn}reputation', 'Ambitious','Boor','Dangerous','Entertaining','Honest','Loafer','Oddball','Repulsive','Respected','Wise') redis.call('SADD', '{cairn}misfortunes', 'Abandoned','Addicted','Blackmailed','Condemned','Cursed','Defrauded','Demoted','Discredited','Disowned','Exiled') redis.call('SADD', '{cairn}expeditionarygear', 'Air Bladder','Antitoxin','Cart (+4 slots, bulky)','Chain 10 feet','Dowsing Rod','Fire Oil','Grappling Hook','Large Sack','Large Trap','Lockpicks','Manacles','Pick','Pole 10 feet','Pulley','Animal/Beast Repellent','Rope 25 feet','Spirit Ward','Spyglass','Tinderbox','Wolfsbane') redis.call('SADD', '{cairn}tools', 'Bellows','Bucket','Caltrops','Chalk','Chisel','Cook Pots','Crow Bar','Drill (hand cranked)','Fishing Rod and Tackle','Glue','Grease','Hammer','Hourglass','Metal File','Nails','Net','Saw','Sealant','Shovel','Tongs') redis.call('SADD', '{cairn}trinkets', 'Bottle','Card Deck','Dice Set','Face Paint','Fake Jewels','Horn','Incense','Musical Instrument','Lens','Marbles','Mirror','Quill And Ink','Perfume','Salt Pack','Small Bell','Soap','Sponge','Tar Pot','Twine','Whistle') redis.call('SADD', '{cairn}charactertropes', 'Cleric','Friar','Dowser','Knight','Dwarf','Magic User','Elf','Ranger','Fighter','Thief') redis.call('HMSET', '{cairn}cleric', 'War Hammer (d10, bulky)','','Chainmail (2 Armor, bulky)','','Gauntlets (+1 Armor)','','Cleansing Blade (d6)','','Holy Symbol (Ward once per day)','','Cloak of the Order','') redis.call('HMSET', '{cairn}friar', 'Scepter (d6) 1 slot','','Deceptive Robes (+1 Armor)','','Censer & Holy Water','','Jug of Honey Wine','','Folk Songbook','','Cart (+4 slots, bulky)','') redis.call('HMSET', '{cairn}dowser', 'Sickle (d6)','','Patchwork doublet (+1 Armor)','','Dowsing Rod','','Eyestone (Sense if placed in fresh water)','','Worn Map','','Spyglass','') redis.call('HMSET', '{cairn}knight', 'Long sword (d10, bulky)','','Chainmail (2 Armor, bulky)','','Helmet (+1 Armor)','','Heraldic Cape','','Manacles','','Fine Rope','') redis.call('HMSET', '{cairn}dwarf', 'War Hammer (1d10) 2 slots','','Pinecone Lattice (1 Armor)','','Trowel','','Jar of Forest Ants','','Poisonous mushroom','','Hand Drill','') redis.call('HMSET', '{cairn}magicuser', 'Fizzled Staff (d8, bulky)','','Dagger (d6)','','Spellbook (random spell)','','Spellbook (random spell)','','Ragged clothing (hidden pockets)','','Leycap (x2, see Relics)','','Tobacco Pouch & Pipe','') redis.call('HMSET', '{cairn}elf', 'Elegant Sword (d8)','','Recurve Bow (d8)','','Gilt Clothing (1 Armor)','','Spellbook (Charm or Detect Magic)','','Golden Flute','','Air Bladder','') redis.call('HMSET', '{cairn}ranger', 'Longbow (d8, bulky)','','Hatchet (d6)','','Padded Leathers (1 Armor)','','Large Trap','','Bloodhound | 2 HP, 12 DEX, bite (d6)','','Thundering Horn','') redis.call('HMSET', '{cairn}fighter', 'Glaive (d10, bulky)','','Helmet and Shield (2 armor)','','Shortsword (d6)','','Shortsword (d6)','','Chain 10 feet','') redis.call('HMSET', '{cairn}thief', 'Two daggers (d6+d6)','','Hooded Jerkin (1 Armor)','','Lockpicks','','Caltrops','','Grappling Hook','','Metal File','','Dice Set','') redis.call('HMSET', '{cairn}armor', 'None','','None','','None','','Light Leather +1 armor 1 slot','','Brigandine +1 armor 2 slots','','Brigandine +1 armor 2 slots','','Brigandine +1 armor 2 slots','','Brigandine +1 armor 2 slots','','Brigandine +1 armor 2 slots','','Brigandine +1 armor 2 slots','','Brigandine +1 armor 2 slots','','Brigandine +1 armor 2 slots','','Brigandine +1 armor 2 slots','','Brigandine +1 armor 2 slots','','Chainmail +2 armor 2 slots','','Chainmail +2 armor 2 slots','','Chainmail +2 armor 2 slots','','Chainmail +2 armor 2 slots','','Chainmail +2 armor 2 slots','','Platemail +3 armor 2 slots','','Heavy Plate (Suit of Armor) +4 armor 3 slots','') redis.call('HMSET', '{cairn}helmshield', 'None','','None','','None','','None','','None','','None','','None','','None','','None','','None','','None','','None','','None','','Helmet +1 armor 1 slot','','Helmet +1 armor 1 slot','','Helmet +1 armor 1 slot','','Sheild +1 armor 1 slot','','Sheild +1 armor 1 slot','','Sheild +1 armor 1 slot','','Sheild and Helmet +2 armor 2 slots','') redis.call('HMSET', '{cairn}weapon', 'Dagger (1d4) 1/2 slot','','Cudgel (1d6) 1 slot','','Staff (1d6) 1 slot','','Dagger (1d4) 1/2 slot','','Staff (1d6) 1 slot','','Cudgel (1d6) 1 slot','','Sword (1d8) 1 slot','','Mace (1d8) 1 slot','','Axe (1d8) 1 slot','','Sword (1d8) 1 slot','','Mace (1d8) 1 slot','','Axe (1d8) 1 slot','','Sword (1d8) 1 slot','','Shortbow (1d6) 1 slot','','Mace (1d8) 1 slot','','Axe (1d8) 1 slot','','Shortbow (1d6) 1 slot','','Light Crossbow (1d6) 1 slot','','Sling (1d4) 1/2 slot','','Crossbow (1d8) 2 slots','','Sling (1d4) 1/2 slot','','Halberd (1d10) 2 slots','','War Hammer (1d10) 2 slots','','Battle Axe (1d10) 2 slots','','Longbow (1d10) 2 slots','','Two-handed Great Sword (1d12) 3 slots','') return 'Data for Cairn loaded Successfully'" 1 {cairn}
```

******************************************
Here are a couple of lua scripts that can be run to create a Cairn character.

This first script will only Roll for Statistic: STR, DEX, and WIL:
This will return 3 values - assign them as you like (in any order) to your stats.
### The following script takes 3 arguments:
1. the number of unique redis key slot-assignment values to expect when running the script
2. the slot-assignment or routing value for this execution (in this case it is the same as what was used to populate all the data)
3. The name to be used as the beginning of the Hashkey Name for the character data being generated (below I use the name Trey)
```
EVAL "local str = 0 local dex = 0 local wil = 0 for x=1,3 do local stat = 0 for i=1,4 do stat=stat + redis.call('SRANDMEMBER','{cairn}d6') end stat = stat -redis.call('SRANDMEMBER','{cairn}d4') if stat>17 then stat = 18 end redis.call('HSET',ARGV[1]..':chardata:{cairn}',x,stat) end return redis.call('HVALS',ARGV[1]..':chardata:{cairn}')" 1 {cairn} Trey
```

After the above is called, aside from the immediate response which comes back, a Hash object is created that holds the values generated.  You can find the full name of the key in Redis by using the Scan command:
```
> SCAN 0 MATCH Trey* COUNT 10000
1) "0"
2) 1) "Trey:chardata:{cairn}"
```
To view all the data currently in that Hash you can execute:
```
> HGETALL "Trey:chardata:{cairn}"
1) "1"
2) "14"
3) "2"
4) "14"
5) "3"
6) "12"
```
This Redis command returns the nested KeyNames and Values assigned to each one.  Because this simple script generates 3 random characteristic numbers and the intent is to allow the user to assigne them to any characteristic they prefer, their names in the Hash are simply: 1, 2, 3    

### What follows is a more complete LUA script that generates character traits and weapons and Armor as well as the above mentioned stats:
************************************
As with the simpler LUA script above, this one takes 3 arguments:
1. How many unique slot-assignment or routing values to expect and use
2. What that routing value will be
3. The Name to use when building the resulting Hash object that holds the generated data

```
EVAL "local str = 0 local dex = 0 local wil = 0 for x=1,3 do local stat = 0 for i=1,4 do stat=stat + redis.call('SRANDMEMBER','{cairn}d6') end stat = stat -redis.call('SRANDMEMBER','{cairn}d4') if stat>17 then stat = 18 end redis.call('HSET',ARGV[1]..':chardata:{cairn}',x,stat) end redis.call('HSET',ARGV[1]..':chardata:{cairn}','female_fname',redis.call('SRANDMEMBER','{cairn}ffnames')) redis.call('HSET',ARGV[1]..':chardata:{cairn}','male_fname',redis.call('SRANDMEMBER','{cairn}mfnames')) redis.call('HSET',ARGV[1]..':chardata:{cairn}','lastname',redis.call('SRANDMEMBER','{cairn}lnames')) redis.call('HSET',ARGV[1]..':chardata:{cairn}','background',redis.call('SRANDMEMBER','{cairn}backgrounds')) redis.call('HSET',ARGV[1]..':chardata:{cairn}','physique',redis.call('SRANDMEMBER','{cairn}physique')) redis.call('HSET',ARGV[1]..':chardata:{cairn}','skin',redis.call('SRANDMEMBER','{cairn}skin'))  redis.call('HSET',ARGV[1]..':chardata:{cairn}','hair',redis.call('SRANDMEMBER','{cairn}hair'))  redis.call('HSET',ARGV[1]..':chardata:{cairn}','face',redis.call('SRANDMEMBER','{cairn}face'))  redis.call('HSET',ARGV[1]..':chardata:{cairn}','speech',redis.call('SRANDMEMBER','{cairn}speech'))  redis.call('HSET',ARGV[1]..':chardata:{cairn}','clothing',redis.call('SRANDMEMBER','{cairn}clothing'))  redis.call('HSET',ARGV[1]..':chardata:{cairn}','virtue',redis.call('SRANDMEMBER','{cairn}virtue'))   redis.call('HSET',ARGV[1]..':chardata:{cairn}','vice',redis.call('SRANDMEMBER','{cairn}vice'))   redis.call('HSET',ARGV[1]..':chardata:{cairn}','reputation',redis.call('SRANDMEMBER','{cairn}reputation'))  redis.call('HSET',ARGV[1]..':chardata:{cairn}','misfortunes',redis.call('SRANDMEMBER','{cairn}misfortunes'))  redis.call('HSET',ARGV[1]..':chardata:{cairn}','expeditionarygear',redis.call('SRANDMEMBER','{cairn}expeditionarygear'))  redis.call('HSET',ARGV[1]..':chardata:{cairn}','tools',redis.call('SRANDMEMBER','{cairn}tools'))  redis.call('HSET',ARGV[1]..':chardata:{cairn}','trinkets',redis.call('SRANDMEMBER','{cairn}trinkets')) redis.call('HSET',ARGV[1]..':chardata:{cairn}','armor',redis.call('HRANDFIELD','{cairn}armor'))  redis.call('HSET',ARGV[1]..':chardata:{cairn}','helmshield',redis.call('HRANDFIELD','{cairn}helmshield'))  redis.call('HSET',ARGV[1]..':chardata:{cairn}','weapon',redis.call('HRANDFIELD','{cairn}weapon')) redis.call('HSET',ARGV[1]..':chardata:{cairn}','Hit Protection',redis.call('SRANDMEMBER','{cairn}d6'))     return redis.call('HGETALL',ARGV[1]..':chardata:{cairn}')" 1 {cairn} Trey
```
In one instance, the above generated the following data that is stored in the Hashkey - Trey:chardata:{cairn} :
( note that it overwrote the previous 3 values for 1, 2, 3 )
```
1) "1"
2) "18"
3) "2"
4) "12"
5) "3"
6) "13"
7) "female_fname"
8) "Lisabeth"
9) "male_fname"
10) "Grinwit"
11) "lastname"
12) "Sunderman"
13) "background"
14) "Servant"
15) "physique"
16) "Flabby"
17) "skin"
18) "Pockmarked"
19) "hair"
20) "Oily"
21) "face"
22) "Chiseled"
23) "speech"
24) "Droning"
25) "clothing"
26) "Soiled"
27) "virtue"
28) "Gregarious"
29) "vice"
30) "Craven"
31) "reputation"
32) "Oddball"
33) "misfortunes"
34) "Defrauded"
35) "expeditionarygear"
36) "Antitoxin"
37) "tools"
38) "Nails"
39) "trinkets"
40) "Horn"
41) "armor"
42) "Chainmail +2 armor 2 slots"
43) "helmshield"
44) "Sheild +1 armor 1 slot"
45) "weapon"
46) "Cudgel (1d6) 1 slot"
47) "Hit Protection"
48) "4"
```

******************************
### Any time a dice needs to be rolled you can issue:
```
SRANDMEMBER {cairn}dX
```

for example:

```
> SRANDMEMBER {cairn}d20
"17"
> SRANDMEMBER {cairn}d6
"5"
> SRANDMEMBER {cairn}d4
"2"
```

Cairn has some pre-defined 'Tropes' 
To select a random character trope:

```
> SRANDMEMBER {cairn}charactertropes
 "Dwarf"
```
To learn what is contained within that Trope:
```
> HKEYS {cairn}dwarf 
1) "War Hammer (1d10) 2 slots" 
2) "Pinecone Lattice (1 Armor)" 
3) "Trowel" 
4) "Jar of Forest Ants" 
5) "Poisonous mushroom" 
6) "Hand Drill"
```

### I imagined only mnaual updates to the generated character data.  In fact, I assumed the information would likely end up on paper. 

To update a previously generated character Hash object with the details of a supplied Trope is something doable with LUA - but some changes would need to be made...

* The data load script would need to assign each of the Trope values to a character-specific attribute - taking into account the variance in how many of a certain attribute might initially exist and how many exist within a Trope.

* Conceptually the LUA script would need to:
1. identify the Hash key containing the trope information (note that in the data load script all such tropes are loaded using all lower-case keynames)
2. identify the Hash key containing the character information to be updated
3. merge the Trope details into the character information Hash Key

### It would be interesting to use JSON instead of Hashes as an exercise in exploring hierachical data managed by LUA ... another enrichment I have not yet implemented


