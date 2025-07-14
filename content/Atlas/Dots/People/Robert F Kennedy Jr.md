---
aliases:
  - RFK
  - RFK jr
  - Kennedy jr
  - Robert F. Kennedy Jr
Category: Source
Class: Person
tags:
  - kennedy-family
  - Vaccine
  - anti-vaccine
  - autism
  - big-pharma
  - Anthony-Fauci
  - wuhan-lab
  - bioweapons
  - hiv-aids
  - thimerosal
  - ivermectin
  - hydroxychloroquine
  - childrens-health-defense
  - environmental-law
  - health-policy
  - Covid-19
  - 5g
  - cia
  - ultra-processed-foods
  - Obesity
  - trump-administration
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