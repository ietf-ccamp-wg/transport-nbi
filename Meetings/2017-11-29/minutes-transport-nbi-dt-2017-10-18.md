# Weekly Call (November 29, 2017)

## Attendees
- Italo Busi  
- Daniel King  
- Dieter Beller  
- Calo Perocchio  
- Haomian Zheng  
- Xiaobing Niu  
- Yuji Tochio  
- Young Lee   

## Agenda:
1) Terminology Review
2) Merging Analysis I-Ds
3) JSON code review
4) Review of TE tutorial
5) Inter-domain link stitching
6) AOB

## Meeting Notes:

### 1) Terminology Review
We have to be careful with the term Use Cases because IESG is not going to publish any longer as RFC use cases.
What we actually doing is an Applicability Statement or Implementation Guideline. We have a WG document just describing the scenarios we wish to address and other drafts providing the Applicability Statement for these scenarios.

We can merge everything in a single Applicability Statement document.

Sergio has provided initial comments to the Use Cases Description WG document  
We can also re-use some terminology and definitions from the TE Tutorial document Principles:
- if there is a term that is already defined in another draft/RFC, we can re-use it and reference to the source document for the definition  
- if some term is missing, we should clarify its definition and see if that definition can be included in other documents or on the DT document  
  
**Actions:**  
- Continue to review of the terminology in the Use Cases Description (I-D), Sergio is leading this action with support from Dan

### 2) Merging Analysis I-Ds
- We plan to merge the three DT documents into a single document  
- This would address a number of overlaps that currently exist between the documents  
  
**Actions:**
- All to review the ToC proposal for the merged I-D sent by Italo on 29 Nov  
- Italo/Daniel to check with CCAMP chairs about this plan considering that one of the document is already a WG while the other two are individual documents  
- Italo to provide the merged document by earlier next week, in time for dicussion on our next T-NBI call (6 Dec)

### 3) JSON code review
Proposed updated JSON code for the ODU Topology in open pull request:
[https://github.com/danielkinguk/transport-nbi/pull/15](https://github.com/danielkinguk/transport-nbi/pull/15)

Proposed updated JSON code for ODU Tunnel Segment Setup in merged pull request:
[https://github.com/danielkinguk/transport-nbi/pull/11](https://github.com/danielkinguk/transport-nbi/pull/11)
      
Latest version of the files:
[https://github.com/danielkinguk/transport-nbi/blob/master/Internet-Drafts/Use-Case-1-Analysis/01/use-case-1-odu2-service-named-explicit-path.json](https://github.com/danielkinguk/transport-nbi/blob/master/Internet-Drafts/Use-Case-1-Analysis/01/use-case-1-odu2-service-named-explicit-path.json)
[https://github.com/danielkinguk/transport-nbi/blob/master/Internet-Drafts/Use-Case-1-Analysis/01/use-case-1-odu2-service-01.json](https://github.com/danielkinguk/transport-nbi/blob/master/Internet-Drafts/Use-Case-1-Analysis/01/use-case-1-odu2-service-01.json)

**Actions:**
- We need a code review and conformance test for the current files - Carlo will do a validation test  
- We would also like a content review - Need a volunteer

### 4) Review of TE tutorial
Daniel has started reviewing the TE Tutorial and it seems very useful for the work of the DT  
We could use the TE Tutorial as a reference for our work
We need to complement on how we use technology-specific (e.g., OTN) models in addition to the TE models  
Also some material in the DT document may be an useful input to the TE Tutorial  
  
**Actions:**  
- Daniel/Italo: continue to review the TE Tutorial
- Daniel/Italo: discuss offline with the authors of the TE Tutorial to agree on the relationships between the two documents

### 5) Inter-domain link stitching
- Need to consider what types of links (and assuming this is all the same layer)  
- Do we need anything beyind the discovery/capability mechanisms that exist (LMP - [https://tools.ietf.org/html/rfc4204)](https://tools.ietf.org/html/rfc4204)),  LLDP, Static .)   
- Where are texisting requiments defined? See G.7714.1/Y.1705.1: [file:///C:/Users/danielking.net/Downloads/T-REC-G.7714.1-201708-I](file:///C:/Users/danielking.net/Downloads/T-REC-G.7714.1-201708-I)!!PDF-E.pdf)  
- Do we need to have a globally unique ID? If its static/manual a discovery mechanism would not be needed?  
- This problem is not only specific to our scenarios/technology, this is an open issue for other technologies as well  
- Suggestion to stick to static/manual configuration for our current applicability statement and then state that discovery mechanisms are out of scope for now, and we can see if anyone would like to work on a seperate document(s) for extending an existing discovery method  
  
**Conclusion:**
Our applibility statement for scneario 3 (use case 3) will state that the ID on PNC and on MDSC is manually configured. We will need some ASCII art to show how this works.   
  
A seperate document that would dicuss inter-domain link stiching discovery (procedure and extensions) in context of ACTN  
- Define and use "TE inter-domain plug" and ensuring a network-wide globally unique value, collision detection etc.  
- How to address we address interoprability of multiple vendors using different methods (static, dynamic - LMP, LLDP, et al.)  

### 6) AOB
Next call is planned on December 6, 2017 at 3-5pm CET  

## Note Takers
- Daniel King  
- Italo Busi  
