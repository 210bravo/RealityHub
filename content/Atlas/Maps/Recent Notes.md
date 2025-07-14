---
up:
  - "[[Home]]"
related: []
created: 2025-06-15
in:
  - "[[Views]]"
---

This **Add** note isn't just an inbox. It's a cooling pad 🧊.
Thoughts come in hot. But after a few days, they cool down.
When cooler thoughts prevail, you can better prioritize. Cool?

> [!activity]+ ## **+** Recent Stuff
> This view looks at the 10 newest notes in your **+** folder. As you process each note: add a link, add details, move them to the best folder, and delete everything that no longer sparks ✨.
>
> ```dataview
> TABLE WITHOUT ID
>  file.link as "",
>  (date(today) - file.cday).day as "Days alive", file.folder
>
> FROM "+"
>
> SORT file.cday desc
>
> LIMIT 10
> ```

> [!activity]+ ## All Recent Stuff
> This view looks at the 10 newest notes in all folders. As you process each note: add a link, add details, move them to the best folder, and delete everything that no longer sparks ✨.
>
> ```dataview
> TABLE WITHOUT ID
>  file.link as "",
>  (date(today) - file.cday).day as "Days alive", file.folder
>
> FROM ""
>
> SORT file.cday desc
>
> LIMIT 10
> ```