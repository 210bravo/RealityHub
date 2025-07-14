---
up:
  - "[[Home]]"
related: "[[Views]]"
created: 2025-06-15
tags:
---
To learn more, visit [[MOCs Overview]]

> [!map]+ # Maps
> This note collects all notes where the `in` property says `Maps`. 
> 
> ```dataview
> TABLE WITHOUT ID
> 	file.link as Map
> WHERE
> 	contains(in,this.file.link) and
> 	!contains(file.name, "Template")
> SORT file.name asc
> LIMIT 222
> ```