---
aliases:
  - "@Kevin_McKernan"
Category: Source
Class: Person
Website:
Twitter: https://x.com/Kevin_McKernan
Substack: https://anandamide.substack.com/
tags:
  - Amyloidogenesis
  - biodefense
  - biotechnology
  - blockchain-technology
  - cannabis-genomics
  - centralized-control
  - Covid-19
  - dna-contamination
  - dna-sequencing
  - federal-reserve
  - fiat-science
  - genomics
  - human-genome-project
  - igg4-immune-modulation
  - lipid-nanoparticles
  - medicinal-genomics
  - mrna-vaccines
  - p53-translation
  - pcr-testing
  - pharmaceutical-industry
  - public-health
  - regulatory-oversight
  - sars-cov-2
  - SV40
  - Cancers
  - Vaccine
  - Vaccine
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