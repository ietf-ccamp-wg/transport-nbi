# Transport NBI DT @ IETF 100 - November 16, 2017

## Attendees

- Italo Busi  
- Daniel King  
- Aihua Guo  
- Yunbin Xu  
- Dieter Beller  
- Sergio Belotti  
- Zheyu Fan  
- Haomian Zheng  
- Qilei Wang  
- Xiaobing Niu  
- Michael Scharf  

## Agenda:

1) Status update after CCAMP WG discussion  
2) AOB  

## Meeting Notes:

### 1) Status update after CCAMP WG discussion

#### 1.1) General Comments  

- Detailed Use case work will later come to the 'applicability statement' or 'Implementation Guideline', by providing how to use IETF YANG models.   
- Near term focus will be on UC1 (single layer, single domain) and UC3 (single-layer, multi-domain)   

#### 1.2) Inter-domain Link Stiching  

- Need to consider what types of links, this will impact discovery/capability mechanisms:
o LMP: [https://tools.ietf.org/html/rfc4204)](https://tools.ietf.org/html/rfc4204)
o LLDP
o Static
o G7714.1: http://www.itu.int/rec/T-REC-G.7714.1
- Assumed inter-domain links are same layer  
- Inter-domain Plug ID will need to be globally unique, how to ensure this happens during the auto-discovery process is part of a specific implementation  
- We can state in the I-D that discovery is likely to in-band, but out of band is also possible  
- Inter-domain plug IDs may also  be assigned and managed by a central network authority, without using an automated discovery process  
- In context of ACTN association at MDSC  
- Hybrid model would also be supported  
- Topology Discovery Mechanism (inter-domain): From NE level and report to controllers (via PNC to MDSC); or can be triggered by MDSC by using a topology discovery agent;   

***Action: Dan to draft text and send to DT for review (especially from the vendors)***

#### 1.3) EPL, EVPL Associations, including access link reporting  
- Useful documents that will help T-NBI discussions  
o  "A YANG Data Model for Optical Transport Network Client Signals"  
o  "A YANG Data Model for Client-layer Topology"  
o  "A YANG Data Model for Client-layer Tunnel"  

***Action: Haomian (author of above I-Ds) and Italo describes Ethernet OTN use case model in their documents and we need to reference this in our documents, some textual description.***

#### 1.4) Additional/Relevent CCAMP documents that the T-NBI team will need to consider/review  
- "TE Topology and Tunnel Modeling for Transport Networks"  
***Action: Italo and Dan to review the TE Model Tutorial and  "TE Topology and Tunnel Modeling for Transport Networks"***

-  "Service Models Explained", although this is IP focused, how do you model transpot service delivery?  

#### 1.5) Protection and Restoration  
- Need from vendors and operators to describe both Protection and Restoration scenarios. Commonality existings across UC1 and UC3, so we can combine text.  

#### 1.6) Merging UC1 and UC3  
- Need to agree plan for new I-D  

***Action: For UC editors to merge UC I-Ds by next DT meeting (29th Nov)***

### 2) Any Other Business

- Michael highlighted that it is not clear how UC4 would be solved using the TEAS TE Topo/Tunnel model in the context of ACTN   
- Should the T-NBI DT be working on IP over optical UC? Currently, our focus is optical transport  

***Action: Michael will provide examples that describes the IP/MPLS over OTN use case, we can then review the scenario as part of the DT intially***

### Actions and Plan for Next Steps

- Agreed that we are developing are not Use Cases but Applicability Statements or Implementation Guidelines. Need to clarify the scope.  
- Agreed that we need to focus on fewer use cases  
- Agred next T-NBI DT meeting  
- Agreed that we will have an occasional T-NBI call that is optimised for Asia-Pac region  
may not be accurate enough.  

***Action: Terminology - Sergio will review and refresh the terminology section, like 'service model' and 'UNI'***

***Action: OpenConfig - DIeter to review their OTN model to see if its relevent for us? How do they map client services?***

## Note Takers

- Italo Busi  
- Daniel King  