# Ambient Intelligence - Assignment 1: Ontology of a library

## Students/IDs
Canella Simone - xxxxxxxx | Isaia Samuele - xxxxxxxx | Daneri Gregorio - 5658523

## Environment
The environment described is a library with four possible types of areas:
- PublicZone: an area without particular features, and that can be accessed by anyone.
- MonitoredZone: an area survailled by PIR sensors and/or door contact sensors, but accessible by anyone.
- CrowdedZone: any area which hosts more than 3 different people.
- RestrictedZone: an area whose access is restricted by a badge reader.

The environment is populated by three different categories of people:
- Librarian: an individual who works at the library, and, thus, who has access to all areas, even resctricted ones.
- Student: a person who has access only to public areas.

## Conlclusions produced by the reasoner
These are the facts inferred by the reasoner about individuals:
- People, who have a badge, can enter areas flagged as restricted.
    - Generates from the rule Person(?p), carriesBadge(?p, ?b), grantsAccessTo(?b, ?r) -> canEnter(?p, ?r)
    - Inferred result: the person obtains a canEnter object property with an instance of a room.

- People, who are inside a room with PIR or door contact sensors, are monitored by those sensors.
    - Generates from the rule Person(?p), isIn(?p, ?r), Sensor(?s), installedIn(?s, ?r) -> detectedBy(?p, ?s)
    - Inferred result: the person obtains a monitoredBy object property with an instance of a PIR or door contact sensor.

- Areas, which have PIR or door contact sensors installed inside, are monitored by those sensors.
    - Generates from the concept axiom (TBox) MonitoredArea = Place
    and ((hostsSensor some DoorContactSensor) or (hostsSensor some PresenceSensor))
    - Inferred result: the individual area becomes of type MonitoredZone.

- Areas, which hosts more than 3 different individauls, are flagged as crowded.
    - Generates from the concept axiom (TBox) Place
    and (hosts min 3 Person)
    - Inferred result: the individual area becomes of type CrowdedZone.