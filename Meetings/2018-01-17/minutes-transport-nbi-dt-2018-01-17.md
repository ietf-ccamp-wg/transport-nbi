Weekly Call (January 17, 2017)
==============================

  

Attendees
---------

- Sergio Belotti  
- Nichael Scharf  
- Carlo Perocchio  
- Giuseppe Fioccola  
- Igor Bryskin  
- Italo Busi  
- Young Lee  
- Daniel King  
- Yuji Tochio  
- Gianmarco Bruno  
 
Agenda:
-------

  
1) Packet/Optical Multi-layer Modelling with ACTN  
2) Merged Internet-Draft  
3) Next Steps  
4) AOB  
  

Meeting Notes:
--------------

### 1) Packet/Optical Multi-layer Modelling with ACTN

  
Slides provided by Michael: [https://github.com/danielkinguk/transport-nbi/blob/master/Meetings/2018-01-17/2018-01-17\_multilayer\_modelling.pdf](https://github.com/danielkinguk/transport-nbi/blob/master/Meetings/2018-01-17/2018-01-17_multilayer_modelling.pdf)  
  
The slides have the purpose to clarify discussion taken during IETF about multi-layer issues in the ACTN architecture.  
  
\- (Slide 2) General comment from Igor stating that TE Topo and Tunnel YANG models, are tools available for ACTN  
\- (Slide 2) Framework I-D contains some example architectures for different MLN scenarios, which can be solved using existing YANG models against the ACTN architectures  
\- (Slide 2) Michael cited a lack of examples showing detailed applicability of ACTN architecture and YANG models, to solve some scenarios that are not clear.  
\- Even in the case of single operator , you can have different organizations delaing with different layer for overlay , underlay relation, moreover you could in principle also to have multiple overlay over underlay.  
\- Which layer should be responsible for overall TE decisions? A discussion on if the MDSC or something else, would be responsible for overal path decision making. Likely that each layer might want to compute based on a specific objective function relevent to its own layer.  
\- How is a lower-layer service path violation (disjoint required, but not achieved or minimum latency) communicated to upper layers requesting the end-to-end service? Seems to be an outstanding issue.  
\- The point (slide 5) is to correlate attribute in the underlay path with any higher link of the overlay (e.g. SRLG as shown in the slide).  
  
**Action**: Do we need a new ACTN Applicability I-D, clearly discussing how the architecture would be implemented against a specific scenario and which models would be applied, and how? This could be IP over Optical.

**Action**: Do we have the existing capability to communicate lower-layer path violations (delay, SRLG, etc.) in multi-vendor / multi-technology enviroments?    
  
The key concern is that abstraction is not possible in the overlay controllers' hierarchy if the top-level MDSC should be responsible for the multi-layer coordination. This is due to tha fact that with overlay abstraction not exposing internal links/nodes , it is not possible to coordinate attribute (like SRLG) implying to know internal links at overlay NW.

**Action**: need to validate the concern  
  
The issue is applicable to any multi-layer overlay/underlay relationship but, in practise, it seems that IP and Optical Integration is the most common scenario. Michael suggests to look at the Open Line System.  
  
**Action**: investigate if there are other multi-layer overlay/underlay scenarios  
  

### 2) Merged Internet-Draft

  
Initial version of the merged draft available on GitHub:  
  
[https://github.com/danielkinguk/transport-nbi/pull/16](https://github.com/danielkinguk/transport-nbi/pull/16)  
  
Under review among co-editors. Early comments are welcome.  
  
The intention is also to change the name of the draft to draft-ietf-ccamp-transport-nbi-applicability-statement  
  
Discussion is still on-going about the process to follow to merge two Individual drafts and one WG draft  
  

### 3) Next Steps

  
Status update of the pending action points on GitHub  
  
The following action points have been assigned and updates are expected for the next DT call:  
\- Terminology review (Sergio): [https://github.com/danielkinguk/transport-nbi/issues/17](https://github.com/danielkinguk/transport-nbi/issues/17)  
\- Review of the initial proposal for the merged I-D (Editors/all): [https://github.com/danielkinguk/transport-nbi/pull/16](https://github.com/danielkinguk/transport-nbi/pull/16)  
\- Relationship with the TE Tutorial in TEAS (Italo/Daniel): [https://github.com/danielkinguk/transport-nbi/issues/19](https://github.com/danielkinguk/transport-nbi/issues/19)  
\- Review of OpenConfig model (Dieter): [https://github.com/danielkinguk/transport-nbi/issues/20](https://github.com/danielkinguk/transport-nbi/issues/20)  
\- Update JSON code based on the feedbacks from TEAS (Italo):   
  
The following action point have been assigned and is still on-going:  
\- Procedure for merging the DT drafts (Italo/Daniel): [https://github.com/danielkinguk/transport-nbi/issues/18](https://github.com/danielkinguk/transport-nbi/issues/18)  
  
The following action point have been assigned but waiting for the merged I-D being published:  
\- Engage with MEF experts (Daniel): [https://github.com/danielkinguk/transport-nbi/issues/21](https://github.com/danielkinguk/transport-nbi/issues/21)  
  
The following action point has not been assigned waiting for a more mature state of the ODUCn control plane framework:  
\- Add considerations about ODUCn: [https://github.com/danielkinguk/transport-nbi/issues/22](https://github.com/danielkinguk/transport-nbi/issues/22)  
  

### 4) AOB

  
Next call is planned on Wednesday January 24, 2018 at 3-5pm CET  
  
Input contributions are solicited to be made available before monday January 22, 2018 at noon CET: this will facilitate preparing the agenda for the call  
  

Note Takers
-----------

- Italo Busi  
- Daniel King  
- Sergio Belotti  
