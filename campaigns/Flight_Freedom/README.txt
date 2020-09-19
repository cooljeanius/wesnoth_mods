So yeah this was another hard one. Here's a writeup on my per-scenario changes:

01 Survival: I didn't actually edit this one my first time thru, but in
  retrospect, if I'm going to be making everything easier, I might as well
  start here.
02a Rebellion: I made it so that the hatchlings get wounded less, to try to
  make it easier to keep them alive
03a Manor: un-commented out code that had weakened some of the guardians and
  instead made it guarded by "ifdef EASY"
04a Caravan: I didn't actually edit this one my first time thru, but since I'm
  taking a second pass at this I figure I might as well edit this one, too, for
  completeness.
05a Blue River: Restricted clippers that Omandro can recruit to 1 on EASY
06a Southern Shore: See note for 04a Caravan above.
07a Open Ocean: Likewise.
08 Landfall: OK this one was a pain. The enemies ganged up on me and just
  wrecked me on my first try, so I tweaked their AIs to try to make them fight
  each other more. Also, tweaks to gold, income, and turns.
10 Underground: This one was too chokepoint-y, so I edited the map to make
  some of the corridors wider, and the terrain more passable for drakes.
  I also added some more villages. I also added a (vague) warning for units
  approaching the statue that revives the skeletal dragon so that players will
  maybe get the idea that they might lose a unit and choose an appropriate one
  accordingly. I didn't want to make it TOO scary of a warning, though, as the
  skeletal dragon is definitely worth the sacrifice, and players should still
  definitely go for it.
11 River of Skulls: Somehow the original 100 turn limit wasn't enough for me,
  so in my rage my first reaction was to set the turns as {TURNS 300 200 100}.
  This gave me such a huge early finish bonus when I finished with these edits
  that it made the next few scenarios probably easier than they should have
  been, so I will have to keep tweaking the turn limit here. I also nerfed all
  the enemies majorly and made them fight against each other more, but there
  might have been some bugs with this, as now only the first few golems
  survive, but none of the farther-in ones do. Also the spider failed to spawn,
  so I added some (untested) code to try to get the dwarves to avoid its
  spawnpoint, but I'm really not looking forward to testing this one again,
  so... well, maybe someone else can help me do some work on it. Also, on EASY,
  I removed the event where the storeroom ceiling caves in on you and kills a
  unit randomly, because, wtf was that doing in there in the first place?
  (update: apparently it was to discourage you from stopping to smell the
  roses, so I edited the message displayed on EASY to that effect.)
  Finally, because the turn limit is increased, I changed the turns on which
  Kogw gives you your progress notifications.
12 Rockfall: Made the dwarves fight the lava monsters. Also gave the player
  more time to escape.
18 Return to Morogor: I had finally run thru my massive gold reserves left
  over from River of Skulls by this point, but since all my spending of it
  previously had given me a large recall list, I needed to add more gold
  again to let me actually use it.
19 Liberation: I actually debugged my way thru this level originally, instead
  of editing it first, so these edits are untested, but they should still
  mostly reflect the debugging commands I used. Basically, I needed to up the
  turn limit again, because the original author liked chokepoints too much.
  I might want to edit the map later to widen some of the corridors...
20 Endgame: These changes aren't all entirely tested, either. Mostly gold
  tweaks. The changes I made to the "enemy gold" event varied the amounts too
  much on difficulty in the changes I actually played thru with, so hopefully
  these newer amounts will be small enough in terms of their differences.

Also, this doesn't exactly fit in any particular scenario, but I gave the
Drake Guard the Steadfast ability, because otherwise at first glance it looks
like a RiPLIB violation.
