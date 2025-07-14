---
aliases:
  - Wiles
Category: Character
Class: Person
Website:
Twitter: https://x.com/SusieWiles
tags:
---
```dataview
TABLE 
  guest AS Guest,
  show AS Show,
  date AS Date
FROM "Youtube_Podcast"
FLATTEN array(guest_1, guest_2, guest_3) AS guest
WHERE 
  contains(this.aliases, guest) OR guest = file.name
SORT date ASC
```