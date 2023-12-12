---
component-id: meetups-knowledge-graph
type: KnowledgeGraph
name: MEETUPS Knowledge Graph
description: MEETUPS Knowledge Graph module with data on historical meetups and related to MEETUPS Pilot
work-package:
- WP4
pilot:
- MEETUPS
project: polifonia-project
resource: https://github.com/polifonia-project/meetups-knowledge-graph/
release-date: 20/07/2022
release-number: v0.1
release link: https://github.com/polifonia-project/meetups-knowledge-graph/releases/tag/v0.1
doi: 10.5281/zenodo.7924618
changelog: https://github.com/polifonia-project/meetups-knowledge-graph/releases/tag/v0.1
licence:
- CC-BY_v4
copyright: "Copyright (c) 2023 MEETUPS @ The Open University"
contributors:
- Alba Morales Tirado <https://github.com/albamoralest>
- Enrico Daga <https://github.com/enridaga>
- Jason Carvalho <https://github.com/JaseMK>
credits:
- https://github.com/albamoralest
- https://github.com/enridaga
related-components:
- informed-by: 
  - meetups-ontology
  - meetups-corpus-collection
- generated-by:
  - meetups-hm-identification
- persona:
  - Ortenz
  - David
  - Sophie
- reuses:
  - sparql-anything-java
  - sparql-anything-cli
---

# MEETUPS Knowledge Graph 

## Musical Meetups Knowledge Graph (MMKG)

[![DOI](https://zenodo.org/badge/588597123.svg)](https://zenodo.org/badge/latestdoi/588597123)

The MEETUPS knowledge graph contains data about historical encounters of people in the musical world in Europe from c. 1800 to c. 1945.


## Knowledge Graph description

The KG was built using data collected from Wikipedia. A total of 33309 biographies of musical artist's web pages were collected [1].
The MMKG data contains evidence that describes historical meetups according to Meetups Ontology [2]. 
We apply knowledge extraction techniques and methods for text processing to recognise, classify and link the entities that are part of a historical meetup, particularly: people, places, time expressions and themes.

The MMKG is one of the main components of the MEETUPS Pilot.
MMKG is one of the main components of the MEETUPS Pilot.
Here are the links to important components related to the KG.
1. [Meetups Corpus Collection](https://github.com/polifonia-project/meetups_corpus_collection)
2. [Meetups Ontology](https://github.com/polifonia-project/meetups-ontology)
3. [Meetups Pilot](https://github.com/polifonia-project/meetups-ontology)

## Competency questions related to MMKG

The KG answers the CQs formalised as part of the Meetups Ontology knowledge requirements.

Ortenz
- What places did musician Z visited in her career?
- Where did she perform?
- Where did she live?
- Did musician X and performer Y ever meet? Where, when, and why?
- In what context the meeting happened?
- What is the nature of the event?
- Was it a celebration, a festival, a private event?
- Was it a religious or a secular event?
- Who paid to support the event?
- What is the provenance of the event attendees? What and how they happened to be there?
- Did they travel to reach the place?
- Were they invited? Was the meeting accidental?
- How can we characterize the relation among the participants?
- Was there a power relation? (e.g., Patreon / Musician)

## Statistics:

We use SPARQL Anything and design CONSTRUCT mappings, to create triples from each biography. To obtain these statistics we build a series of queries available here
```
queries/statistics_query.sparql
```
```
-------------------------------
| key                 | value |
===============================
| "Biographies"       | 33309 |
| "Meetups"           | 45812 |
| "Persons mentioned" | 49170 |
| "Subjects"          | 16748 |
| "Places mentions"   | 7107  |
| "Time expressions"  | 51120 |
-------------------------------
```

It is possible to use SPARQL Anything to generate the same statistics using the CSV-generated
```
$ fx -q queries/statistics.sparql -l data/meetups/
```

## KG construction

### Pre-requirements

The KG is built using the output of the knowledge construction pipeline. 
To run the following commands, first:
- Download the SPARQL Anything command line from the [project release page]https://github.com/SPARQL-Anything/sparql.anything/releases.
SPARQL Anything requires Java >= 11. We used the  sparql-anything-0.8.1 version
- Download the CSV files generated as output of the [Knowledge extraction pipeline]https://github.com/polifonia-project/meetups_pilot
	- Folders: 
- Download the CONSTRUCT mapping scripts from 
	- script 1
	- script 2
	
### Commands

Generate a list of biographies and related files.
```
fx -q queries/list-sample.sparql -o data/biographies.csv -f CSV
```
Generate sentences KG data
```
fx -q queries/sentences.sparql -i data/biographies.csv -p "data/sentences/?fileId.ttl" -f TTL
```

[part above to be updated...]

```
fx -q queries/sentences.sparql -v fileId=10085 -v subject=http://dbpedia.org/resource/Edward_Elgar
```

Last step: generate `meetups_quads` from `meetups_triples` and `list-of-biographies.csv`:
```
fx -q queries/generate_nq_each.sparql -v data/list-of-biographies.csv -f NQ -p "./data/meetups_quads/?id.nq"
```

## Meetups KG extraction: summary

## Repository structure

The meetups 

## MELODY data stories

To be released in the next deliverable



## Acknowledgements

This work was supported by the EU’s Horizon Europe research and innovation
programme within the Polifonia project (grant agreement N. 101004746).
