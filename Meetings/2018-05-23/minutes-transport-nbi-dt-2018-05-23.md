# Weekly Call (May 23, 2018)

## Attendees
- Italo Busi  
- Sergio Belotti  
- Gianmarco Bruno  
- Yuji Tochio  

## Agenda:
1) ODU2 and EPL Service Examples  
2) I2RS Topology attributes  
3) AOB  
  
## Meeting Notes:

### 1) ODU2 and EPL Service Examples

[Pull request #29](https://github.com/danielkinguk/transport-nbi/pull/29)  

Thanks to Gianmarco for the review and fixes to the JSON codes  
  
The mpi1-odu2-service-config.json and mpi1-odu2-tunnel-config.json JSON examples have been reviewed and updated:  
\- need to update the REST operation description to avoid replacing the whole te datastore  
\- not yet clear whether th ietf-otn-tunnel:payload-treatment attribute is needed  
\- the information provided by the src-tpn, src-tsg, src-tributary-slot-count, src-tributary-slots, dst-tpn, dst-tsg, dst-tributary-slot-count and dst-tributary-slots should be provided by the label hop  
\- agreed that the te-bandwidth should provide the information that this is an ODU2 tunnel (waiting for OTN Tunnel model updates)  
\- aligned with the latest proposal by the TE Tunnel model authors on how to use the path-scope in this case  
\- the proposal for settin the direction attribute of numbered/unnumbered hop has been accepted  
\- not clear how to set teh te-label-direction  
  
**Action (Italo): update the REST operation to avoid replacing the whole te datastore**  
**Action (Italo): check with TE Tunnel model authors why the source and destination attributes are defined as ip-address and not as te-node-id**  
**Action (Sergio): check the need for the ietf-otn-tunnel:payload-treatment attribute**  
**Action (Italo): check with OTN Tunnel model authors if the src-tpn, src-tsg, src-tributary-slot-count, src-tributary-slots, dst-tpn, dst-tsg, dst-tributary-slot-count and dst-tributary-slots attributes/containers should be removed**  
**Action (Italo): check with TE Tunnel model authors how to set the te-label direction**  
  
These JSON examples cannot be validated because the latest version of the OTN Tunnel model is not compatible with the latest version of the TE Tunnel model. We will wait for the next update of the OTN Tunnel model before completing the work.  
  
The mpi1-epl-service-config.json and mpi1-otn-topology.json JSON examples have been reviewed with no changes. These JSON examples have been validated and trimmed by Gianmarco prior to the DT call so they are ready to be copied within the Internet-Draft.  
  
**Action (Carlo, Gianmarco, Haomian and Sergio) - Provide feedbacks to the github pull request review request. After that, the pull request will be merged in the master branch.**  

### 2) I2RS Topology attributes

[Pull request #10](https://github.com/danielkinguk/transport-nbi/pull/10)  

This discussion has been postponed to the next DT call  

### 3) AOB

Next DT call is scheduled for June 6, 2018 at 3pm CEST  
 
# Note Takers
- Italo Busi  
