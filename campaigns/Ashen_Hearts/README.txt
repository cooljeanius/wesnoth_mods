Things got tough from 05 (Runic Gate) onwards. The turn limit in Runic Gate
was way too short, and plus I hadn't promoted any Thrashers or Enforcers
yet, so I made them manually recruitable. In 06 (Tears of the Heartfangs) I
was actually able to complete it as is, but since I had to edit it anyways
to disallow recruiting of the Thrashers and Enforcers I had allowed to be
recruited in the previous scenario, I noticed some other things I wanted to
change, too, while I was at it, such as making it easier to unfreeze Malkrath,
which meant I made Arbiters recruitable, which meant I'd have to edit the next
scenario, too, to disallow them again. Of course I would have had to have
edited the next one, i.e. 07 (Dragonheart) anyways to make it easier, since
the Dwarves were wrecking me. I discovered that if you do
LIMIT_CONTEMPORANEOUS_RECRUITS on a unit that isn't actually recruitable, it
becomes recruitable again, which is why Thunderguards were showing up even
though they weren't actually in the recruit list. Setting the value of
LIMIT_CONTEMPORANEOUS_RECRUITS to 0 instead of 1 disabled them again. I also
made Uluthur able to recruit, since there was a keep that seemed made perfectly
for him, and in the process I discovered an interesting issue with ellipses
that Iris helped me fix on Discord. I don't think I actually needed to edit
08 (Ilrandh) but I did anyways just for completeness. 
