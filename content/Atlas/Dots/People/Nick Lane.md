---
aliases:
Category: Source
Class: Person
Website:
Twitter:
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
Author of [[Power-Sex-Suicide_Mitochondria and the meaning of life]] 