---
up:
  - "[[Sources]]"
related: 
created: 2025-06-15
---
This note passively looks at the properties of Sources. If a note has an `in` property that includes a link to `Books`, it will show up below.

```dataview
table Author, Status
from "Atlas/Dots/Sources"
where type = "Book"
sort Date asc
```