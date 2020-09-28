This one got hard eventually; the author seemed to assume that the player
would do a better job keeping their units alive than I did. Actually, the
author seemed to make a lot of assumptions about player behavior that didn't
necessarily hold true in general. I might have to take a second pass at this,
as there's a lot of other cleanups to be done, too:

 - switching commenting-out of code to ifdef-ing out of code, or just removing
   it
 - "Khalifate" to "Dunefolk" renaming
 - varying more quantities by difficulty
 - general copyediting of text (it's mostly pretty well-written for a work
   authored by a non-native English speaker, but there's a lot of text, and
   typos slip thru...)

Anyways, here are my per-scenario notes:

05 The Swamp Things: ADVICES.txt says it's not supposed to be hard, and that
  it's "easily winnable with proper tactics (and enough high-level loyal
  akladians)". Well guess what, I didn't have enough high-level loyal
  Akladians. Or any leftover Akladians, for that matter. Or even any gold.
  This is one of those examples of what I'm talking about when I say the author
  makes incorrect assumptions about player performance. If I don't have as many
  recalls or as much gold as an author is expecting me to have to be able to
  complete a scenario, I'm not going to go back and replay previous scenarios
  to try to do better, I'm just going to edit the offending scenario until it's
  easy enough for me to complete with my current save status. My opinion is
  that all campaigns should be balanced for the worst-case scenario where the
  player comes into the scenario (heh, other sense of the word) with an empty
  recall list and no gold carryover, at least on EASY. Anyways, as for my
  actual changes to this scenario, it was a mixture of gold/turns tweaks, plus
  using the LIMIT_CONTEMPORANEOUS_RECRUITS macro, plus reducing AI aggression
  (along with other AI tweaks).
10 Siege of Haeltin: gold/income tweaks, vary STARTING_VILLAGES radius with
  difficulty, other misc. changes
14d Avenging Ruen: I forget
17 Sneaking out of Raedwood: I forget
19a The Woods of Okladia: I think this was around where enemy sides started
  to get Wondermen, and since they are extremely deadly, I had to put a limit
  on them, and let the enemy Akladians recruit Holymen as an alternate healer
  instead. (I also did likewise in later scenarios)
19c The Oracle: I varied all the starting units' hitpoints and experience with
  difficulty.
21a Abducted Bride: I gave the player consolation units for any missing recalls
  they might have, and also added some extra villages.
22 Leaving Okladia: Lots of tweaks; hard to summarize
23 Trapped: Made it easier to hire the Dunefolk and made it more rewarding to
  do so.
25 The Awakening: Gave the AI some other goals besides just targeting Gawen,
  to prevent Huon from getting to their leaders before you do.
27 Orannon: Prevent Mal-Raylal from reviving on EASY; lots of other changes,
  too.

Also, I forget which scenario this was, but there was a point in the campaign
where you were reduced to only being able to recruit peasants, and I got tired
of that and added back the ability to recruit fencers earlier than was
intended, so now I'll probably want to edit a message in S24 (Fall of Freetown)
to reflect that (I didn't do that my first time thru though, because it's a
story-only scenario)

I'm thinking of making a separate add-on for all the edits I want to make,
since there are a lot, but that might be harder than making an add-on out of
SotBE, since that was copying over a campaign from mainline, but this would be
copying a much-bigger add-on that's already in my add-ons directory and comes
with other stuff besides just the campaign...
