---
aliases:
  - Carroll
  - Ian Carol
Class: Person
Category: Source
Website: https://canceliancarroll.com/
Twitter: https://x.com/IanCarrollShow
tags:
---
```dataview
TABLE 
  guest AS Guest,
  show AS Show,
  date AS Date
FROM "Youtube_Podcast"
FLATTEN array(guest_1, guest_2, guest_3) AS guest
WHERE guest = this.file.name OR contains(this.aliases, guest)
SORT date ASC
```