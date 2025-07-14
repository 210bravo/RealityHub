---
up:
  - "[[Home]]"
created: 2025-06-15
in:
  - "[[Maps]]"
aliases:
  - Sources Map
---

> [!Book]- ### Audiobooks
> ```dataview
> TABLE author AS Author, Status, dateformat(Date, "yyyy") AS Published
> FROM "Atlas/Dots/Sources"
WHERE type = "Audiobook"
> 
> SORT year asc
> ```

> [!Book]- ### Books
> ```dataview
> TABLE author AS Author, Status, dateformat(Date, "yyyy") AS Published
> FROM "Atlas/Dots/Sources"
WHERE type = "Book"
> 
> SORT year asc
> ```

> [!Book]- ### Videos
> ```dataview
> TABLE author AS Author, Status, dateformat(Date, "yyyy") AS Published
> FROM "Atlas/Dots/Sources"
WHERE type = "video, youtube, rumble"
> 
> SORT year asc
> ```

---

- [[Books]] | [[Videos]] | [[Podcasts]] | [[Threads]] | [[Audiobooks]] | [[Articles]] | [[Speeches]] 

> [!Script]- ### All Sources
> ```dataview
> TABLE author AS Author, Status, dateformat(Date, "yyyy") AS Published
> FROM "Atlas/Dots/Sources"
> WHERE fileClass = "Source"
> SORT date(Date).year ASC
> ```