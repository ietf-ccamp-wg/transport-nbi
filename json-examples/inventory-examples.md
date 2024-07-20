# Examples of inventory model for transport networks

## Equipment Sites

Two equipment sites are described:
- Wuhan-C-A1 with two equipment rooms:
  - Wuhan-C-A1-NO.101
  - Wuhan-C-A1-NO.102
- Wuhan-C-A2 with one equipment room:
  - Wuhan-C-A2-NO.101

Within the equipment room Wuhan-C-A1-NO.101, four racks in row 1 are considered:
- Rack 1-1: rack 1 in row 1, which is fully occupied by Ne(115-50)
- Rack 1-2: rack 2 in row 1, which is fully occupied by Ne(115-51)
- Rack 1-3: rack 3 in row 1, which is partially occupied by Ne(115-51) and Ne(115-52)
- Rack 1-4: rack 4 in row 1, which is partially occupied by Ne(115-51).

Within the equipment room Wuhan-C-A1-NO.102, two racks in row 1 are considered:
- Rack 1-1: rack 1 in row 1, which is fully occupied by Ne(115-52) and Ne(115-53)
- Rack 1-2: rack 2 in row 1, which is fully occupied by Ne(115-52) and Ne(115-53)

Within the equipment room Wuhan-C-A2-NO.101, two racks in row 1 are considered:
- Rack 1-1: rack 1 in row 1, which is partially occupied by Ne(115-53)
- Rack 1-2: rack 2 in row 1, which is partially occupied by Ne(115-53)

## Network Elements

The following multi-shelf network element examples are described:
- Ne(115-50) which occupies a full rack (rack 1-1 in Wuhan-C-A1-NO.101 equipment room)
- Ne(115-51) which is occupying multiple racks, within the same room, some fully and some partially:
  - rack 1-2 in Wuhan-C-A1-NO.101 is fully occupied;
  - rack 1-3 in Wuhan-C-A1-NO.101 is partially occupied and shared with Ne(115-52);
  - rack 1-4 in Wuhan-C-A1-NO.101 is partially occupied but not yet shared with any other NE
- Ne(115-52) which is occupying multiple racks in multiple rooms within the same site;
- Ne(155-53) which is occupying multiple racks in multiple rooms in multiple sites.

### Chassis Locations

The location of a chassis component can be physical (representing the position of the chassis within the physical rack in the equipment room) or logical (representing the position of the chassis component within the network-element)

The relative physical position of a chassis within a rack is represented by the 'rack-relative-position' attribute in the 'contained-chassis', as defined in the 'ietf-ni-location' YANG module of \[I-D.wbbpb-ivy-network-inventory-location].

The logical position of a chassis is represented by a string formatted as defined in in section 4.2 of \[ONF_TR-547] for the INVENTORY_ID property.

The logical position of a chassis is not explicitly reported in the 'ietf-network-inventory' YANG module of \[I-D.ietf-ivy-network-inventory-yang] but it can be built by using the 'name' attribute of the network-element which contains the chassis and the 'parent-rel-pos' attribute of the 'component' which represents the chassis.

The table below describe the association between the physical position and the logical position of the chassis provided in the examples:

| Logical Location | Physical Location |
| --- | --- |
| /ne=Ne(115-50)/sh=1 | Chassis 2 of rack 1 in row 1 of room Wuhan-C-A1-NO.101 |
| /ne=Ne(115-50)/sh=2 | Chassis 3 of rack 1 in row 1 of room Wuhan-C-A1-NO.101 |
| /ne=Ne(115-50)/sh=3 | Chassis 1 of rack 1 in row 1 of room Wuhan-C-A1-NO.101 |

The 'ne-ref' and 'component-ref' attributes in the 'contained-chassis', as defined in the 'ietf-ni-location' YANG module of \[I-D.wbbpb-ivy-network-inventory-location] provides the association between a chassis contained by a physical rack and the corresponding chassis component contained in the network-element.
