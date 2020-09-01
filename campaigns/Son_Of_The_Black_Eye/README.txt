I know this is supposed to be an expert-level campaign, but I still wanted to
beat it anyways, so I had to edit it a lot. I edited it so much that I'm
thinking of publishing my changes as a separate campaign on the add-on server.
Here's a description of my changes:

01 End of Peace: Just some basic gold tweaks. Probably too easy now, but it's
  the first scenario, so it ought to be easy IMO.
02: skipped
03 Toward Mountains of Haag: Just basic gold/turns tweaks again
04 The Siege of Barag Gor: OK now here's where things really start to change.
  The defenders of Barag Gor kept dying before I could save them, so I had to
  make them stronger. The shamans wouldn't hit anything whenever they attacked,
  so I made their attacks magic, partly to increase their hit chances, and
  partly also because that just made more sense to me anyways? Also I put more
  villages inside of Barag Gor for healing, and also because as a city, it just
  made sense to have them. I also made Rugh's death cause defeat, which may
  seem like it makes it harder, but actually it makes it easier by saving you
  the time of just waiting around after he dies for the rest of you to die as
  well, because that's basically what happens when he dies anyways.
05: no changes
06 Black Flag: Here the enemies kept overtaking me before I really had a chance
  to set up, so I removed their starting villages so they'd waste more time
  capturing them instead. I also wanted to give your ally some villages as
  well, but since they don't actually have a leader I don't think it actually
  worked. (The documentation for the STARTING_VILLAGES macro said it "relies
  on the side having a unit with canrecruit-yes at start" and that "if it
  doesn't, you should use STARTING_VILLAGES_AREA instead" which I did, but that
  didn't seem to work either? Maybe I'll make Affman a leader later and set
  `leader_ignores_keep` to `yes` so he keeps attacking anyways as he currently
  does...) Anyways, I also turned the generals into lieutenants in this
  scenario as well.
07 The Desert of Death: It took too long waiting for everyone to get a chance
  to recover from their scorpion poisonings, so I added more villages to the
  map.
08 Silent Forest: basic gold/turns tweaks
09: no changes
10 Saving Inarix: I made it much easier to save Inarix here. I turned Thelarion
  from an Elvish Champion into an Elvish Hero here, and since he keeps coming
  back, I kind of wanted to find a way to track whether he advances a level or
  not and then set his unit type accordingly or not in subsequent scenarios,
  but I haven't figured out how to do that yet. I upgraded Plonk from a Slayer
  to a Nightblade to help you break thru the bottleneck on the bridge more
  easily. I gave Inarix more guards escorting him on easy, which might have
  caused an extra village to get captured that didn't used to be captured
  previously, so I'll want to tweak the x/y coordinates of their spawn location
  if I'm going to put my edits on the add-on server. 
11 Clash of Armies: I reduced the number of gryphons the dwarves recruit here
  so you don't have to split your attention as much and can focus more easily.
  I also reduced the HP boosts for the transport ships so they can be destroyed
  more easily.
12: no changes
13: no changes
14 Back Home: I used the LIMIT_CONTEMPORANEOUS_RECRUITS and ON_DIFFICULTY
  macros here a lot; in retrospect I should probably go back and use the
  ON_DIFFICULTY macro more in previous scenarios where I wrote stuff out
  the long way with ifdefs...
15 Civil War: mostly just some basic turns/gold tweaks. I might go back and
  add back the commented-out assassination code later, but I'll need to find
  a way to give the player a way to sneak around the front lines to actually
  pull off assassinations while the enemy still has other units alive...
16 The Coward: I edited the map here to give the player more keep tiles for
  recruiting, so they can catch up to the stream on enemies flooding them on
  time. Also some gold levels tweaks. In retrospect after the enemy's initial
  assault wears off they're not left with much, so I might want to give them
  an income to make up for the reduction in gold I docked them with.
17 The Human Attack: just gold tweaks.
18 Northern Alliance: again, mostly just gold tweaks. I also tried to make
  Shan Taum more defensive so he'd defend more against Howgarth rather than
  killing your green side of orcish allies, but that didn't really work. I
  mean, it worked in the sense that I saved my allies after I made my edits,
  but Howgarth still got to Shan Taum before me though.
