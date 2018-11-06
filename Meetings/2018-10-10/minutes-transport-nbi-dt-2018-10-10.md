#Weekly Call (October 10, 2018)

##Attendees
- Italo Busi
- Carlo Perocchio
- Gianmarco Bruno
- Haomian Zheng
- Sergio Belotti

##Agenda:

1) Topology Updates
2) Plan for IETF 103
3) AOB

##Meeting Notes:  

###1) Topology Updates  

[Pull request #44](https://github.com/danielkinguk/transport-nbi/pull/44)

Topology (mpi1-otn-topology.json) has been simplified: network-id has been populated and in the future a standardized prefix will be added.

Confirmed that PNCs are not aware of the opposite end of inter-domain and access links.

Remove the domain-id attribute.

Only MDSC is aware of them via configuration exploiting the plug-id mechanism.

Agreed that we have to add example of use plug-id that is still missing:  [Open Issue #45](https://github.com/danielkinguk/transport-nbi/issues/45) 

Full details written in the comments of the pull request.

For further discussion how to model/propagate alarms between PNCs and MDSC: [https://github.com/danielkinguk/transport-nbi/issues/46](https://github.com/danielkinguk/transport-nbi/issues/46)

I-D: editorial changes, clarifications and aligned with the new example.

Issue for the URI schema to to be used with topology identifiers created and assigned to Carlo after last DT call: [Open Issue #41](https://github.com/danielkinguk/transport-nbi/issues/41)

###2) Plan for IETF 103  

Deadline for uploading the draft is 22 October.

Actions to complete:
- review and merge topology updates: [Open Issue #44](https://github.com/danielkinguk/transport-nbi/pull/44)
- complete ODU and EPL service examples at MPI1: [Open Issue #38](https://github.com/danielkinguk/transport-nbi/pull/38)
- address comments discussed at IETF 102: [Open Issue #40](https://github.com/danielkinguk/transport-nbi/issues/40)
- add text to Security and Management sections: [Open Issue #36](https://github.com/danielkinguk/transport-nbi/issues/36)
- full review of the I-D text: [Open Issue #35](https://github.com/danielkinguk/transport-nbi/issues/35)

Actions postponed to IETF 104:

- move Appendix A (tooling) to another I-D: [Open Issue #39](https://github.com/danielkinguk/transport-nbi/issues/39)
- relationship with TE tutorial in TEAS: [Open Issue #19](https://github.com/danielkinguk/transport-nbi/issues/19)

Daniel is going to ask for the presentation slot: [Open Issue #47](https://github.com/danielkinguk/transport-nbi/issues/47)

Italo will arrange the f2f meeting: [Open Issue #48](https://github.com/danielkinguk/transport-nbi/issues/48)

###3) AOB  

Next DT call is planned on October 17, at 4-6pm CEST  

##Note Takers  
- Italo Busi  
- Gianmarco Bruno
