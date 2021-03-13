Beaten. It got rather hard near the end. Scenario-specific notes:
08 Clearwater Port: Yeah Commander Aethyr was kinda suicidal here, so I gave him
  and the player more gold here to make it easier to protect him. Note that I made
  these changes before I knew how to change AI parameters, so if I went back and
  did this one again I might try messing with the AI parameters instead...
14 Rough Landing: Just some minor gold/income tweaks
17a The Dragon: This was the last of the 4 "any order" scenarios I played. The
  saurians were overwhelming me, so I gave the player some more gold and income,
  and some starting villages so that I wouldn't have to waste starting turns
  capturing them. I also reduced enemy gold and income and their starting villages
  radii, so they would have to spend more time capturing them instead of attacking.
  I also gave the player an extra encampment tile on EASY, so that I could recall
  my merfolk a little bit closer to the swamps and thus get them into favorable
  terrain more quickly. I also made the dragon awakening turn vary by difficulty,
  and made the loot vary by difficulty, too.
17b Lizard Beach: This one of the earlier of the 4 "any order" scenarios I played.
  I did the usual turns/gold/income tweaks. Also the giant mudcrawlers were
  overwhelming me with how much they split up into smaller ones, so I did
  LIMIT_CONTEMPORANEOUS_RECRUITS on them (varying by difficulty) and, on EASY, I
  took away the loyalty of the smaller ones they split into, to make them take up
  upkeep.
17c Troll Hole: I tried playing this one both earlier and later in the group of the
  4 "any order" scenarios. I think I tried playing it first, but then gave up and
  came back to it third. I did the usual turns/gold/income tweaks, turned down the
  aggression of the trolls slightly, and gave them fewer starting villages. I also
  tried to give the spiders some traits that would vary by difficulty (ones that
  would nerf them on easier difficulties), but that didn't seem to have worked. I
  also varied the loot amounts by difficulty.
17d Cursed Isle: I actually didn't need to change this one that much; I just edited
  the starting gold because I was doing that for all of them, so I did so, here, as
  well, for completeness.
19 The Vanguard: Usual turns/gold/income tweaks, gave player starting villages,
  reduced orcish starting villages radii with difficulty, slightly reduced orcish
  aggression with difficulty, rewrote variation of loot amounts to use the
  ON_DIFFICULTY macro instead, switched commenting-out of code to ifdef-ing it out
  instead, and stuff.
20 Return of the Fleet: Usual turns/gold/income tweaks, increased player starting
  villages radii with difficulty, reduced enemy starting villages radii with
  difficulty, and stuff.
22 The Rise of Wesnoth: Usual turns/gold/income tweaks; the gold amount for EASY,
  combined with my carryover from previous scenarious, was exactly enough to recall
  my entire recall list (rounded to the nearest 10 units of gold). Also gave the
  player some starting villages, and edited the terrain a bit to give the player
  more recruiting tiles, and also give the player's merfolk a better path to get
  into the river. Also reduced enemy starting village radii with difficulty, and
  made the events where the cuttlefish destroy the bridges turn them into fords
  instead on EASY, to make them less annoying. Also switched commenting-out of code
  to ifdef-ing out of code.
