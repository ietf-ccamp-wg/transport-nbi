# Weekly Call (October 25th, 2017)

## Attendees

* Italo Busi  
* Sergio Belotti  
* Carlo Perocchio  
* Daniel King  
* Dieter Beller  
* Oscar Gonzales de Dios  
* Yuji Tochio  
* Young Lee  

## Agenda:

1) Next steps for Use Cases I-D (just adopted as CCAMP WG document)  
2) Use Case 1 Analysis: doubts about EPL, EVPL and other client services  
3) Use Case 3 Analysis: discussion about inter-domain link stitching  
4) Use Case 1 Analysis: TE Tunnel attributes for ODU2 transit service
5) Use Case 1 Analysis: I2RS topology attributes  
6) AOB  

## Meeting Notes:

### 1) Next steps for Use Cases I-D (just adopted as CCAMP WG document)

Comment received indicating that, as opposed to what is written in the scope, the draft does not contain applicability and gap analysis.  

From September 27th, 2017 DTcall minutes:  
- Recent dicussion with IESG members highlighted the need to ensure we are combining Use Cases and Applicability for our DT output.  
- We will discuss how to structure the work on the analysis documents in the next DT call  
- We need to be clear that we will have companion documents that show solution for the use cases. This is to ensure a smooth path for both the Use Case I-D and Solution/Model I-Ds through IESG. Feedback we received was the IESG are limiting I-Ds/work that only dicuss Use Cases.  

Proposed updated text on GitHub: [https://github.com/danielkinguk/transport-nbi/pull/13](https://github.com/danielkinguk/transport-nbi/pull/13)  

**Actions**
- Dan to Submit new version before IETF100 submission deadline (Monday 30 Oct)

### 2) Use Case 1 Analysis: doubts about EPL, EVPL and other client services

Proposed updated draft on GitHub: [https://github.com/danielkinguk/transport-nbi/pull/12](https://github.com/danielkinguk/transport-nbi/pull/12)  

- Updated (Uploaded on October 24) with initial analysis, and open issues, for the EPL, EVPL and OTN Client Private Line Services  
- Discussion on label assignment issue for tributary interfaces/slots. How does the MDSC discover connection information internal links in ODU topologies? The current model does not provide connectivity information, it may require another model that provides/reports client ethernet connectivity information for access port and ODU tunnel. Figure 2 (ODU2 Transit Tunnel) highlights the issue.  

**Actions**  
- Need to include discussion on ODUCn. This is already under discussion in other WGs and I-Ds  
- Open issue for access links and how tributary interfaces/slot mappings to ODU tunnels are reported   
  - Review Haomian's drafts:
      [https://tools.ietf.org/html/draft-zheng-ccamp-client-topo-yang](https://tools.ietf.org/html/draft-zheng-ccamp-client-topo-yang)  
      [https://tools.ietf.org/html/draft-zheng-ccamp-otn-client-signal-yang](https://tools.ietf.org/html/draft-zheng-ccamp-otn-client-signal-yang)  
  - Review OpenConfig OTN model:  
    [https://github.com/openconfig/public/blob/master/release/models/optical-transport/openconfig-transport-types.yang](https://github.com/openconfig/public/blob/master/release/models/optical-transport/openconfig-transport-types.yang)  
- Add reference to NBI DT charter/members in the I-D   
- Sergio and Young to provide review of current I-D, with Italo's updates, before submission on Monday  
- Upload JSON examples to the GitHub and we will submit new code in the I-D when the submission window opens again on Monday at IETF100   
- The solution proposed in Haomian's drafts can be further developed by the DT (it is understood that the DT is expected to develop technology-speicifc YANG models) 
**- Italo/Daniel to check with CCAMP WG chairs that these drafts would fit into the DT scope**  

Oscar reported that the next update of the TE Topology I-D will provide some guidelines on how technology-specific extensions and the authors will review the new text with those working on technology-specific extensions. DT members are invited to review and comment these guidelines as soon as the updated draft of TE Topology is made available.  

### 3) Use Case 3 Analysis: discussion about inter-domain link stitching

Proposed updated draft on GitHub: [https://github.com/danielkinguk/transport-nbi/pull/9](https://github.com/danielkinguk/transport-nbi/pull/9)  

- The I-D was requiring a description of the inter-domain link stiching  
- Further discussion on access link modeling, how the physical links between transport domains, will also be required in this I-D. Current options:  
    o Preconfigured associations on the MDSC  
    o Configure associations in the adjancent PNCs  
- No current clear agreement.
  Either solution has strengths and weaknesses, this issue needs to be outlined in the document  
- Igor's TE Tunnel Tutorial:
  [https://www.ietf.org/mail-archive/web/teas/current/pdfxypZJgPR2J.pdf](https://www.ietf.org/mail-archive/web/teas/current/pdfxypZJgPR2J.pdf)  

**Actions**
- Carlo/Italo to submit the - 00 version by IETF100 submission deadline

### 4) Use Case 1 Analysis: TE Tunnel attributes for ODU2 transit service

Proposed updates to the JSON code uploaded on GitHub: [https://github.com/danielkinguk/transport-nbi/pull/11](https://github.com/danielkinguk/transport-nbi/pull/11)  

Agreed to split the creation of the named-explicit-path and of the tunnel in two operations.  

Four steps:  
    1) MDSC requests the creation of the named-explicit-path  
    2) MDSC gets the OpState of the named-explicit-path that has been created  
    3) MDSC requests the creation of the tunnel  
    4) MDSC gets the OpState of the created tunnel (including LSP states)  

There will be a different JSON code on each step.  

We can focus on steps 1) and 3) for the next udpate.  

Comment: c/interface-id/link-tp-id/  

Agreed that the hop-type should be STRICT for ingress/egress ports  

Agreed that source and destination should not be present. The PNC can understand that the requested tunnel is a Transit Segment because source, destination, src-tp-id and dst-tp-id attributes are not present.  

**Action (Italo/Sergio/Carlo) - Raise the issue about the bandwidth-generic to TE Tunnel authors**  

The signalling-type syntax is not complete in ietf-te-types. It looks like this attribute is not applicable to the MPI and only applicable to SBI so it needs to be moved to the device model: to be further discussed with TE Tunnel model authors.  

**Action (Italo/Sergio/Carlo) - Raise the issue about the bandwidth-generic to TE Tunnel authors**  

Also the provisioning attribute (there is a typo in the name) also does not seem applicable to the MPI and only applicable to SBI so it needs to be moved to the device model: to be further discussed with TE Tunnel model authors.  

**Action (Italo/Sergio/Carlo) - Raise the issue about the bandwidth-generic to TE Tunnel authors**  

Need further discussions about the ietf-otn-tunnel attributes.  

Remove the // bandwdith comment  

Need to review offline the p2p-primary-path attributes  

### 5) Use Case 1 Analysis: I2RS topology attributes

Initial proposal for I2RS attributes uploaded on GitHub: [https://github.com/danielkinguk/transport-nbi/pull/10](https://github.com/danielkinguk/transport-nbi/pull/10)  

Discusion postponed after IETF 100

### 6) AOB

Actions  
- Italo and Dan to share CCAMP slides with NBi DT list for discussion  
- Dan to setup Doodle Poll for face-to-face discussion at IETF100  
- Next call to be scheduled for November 22 (week following IETF100) - please note the daylight savings change in Europe.   

## Note Takers

- Italo Busi  
- Daniel King  
