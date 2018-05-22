# Weekly Call (April 18, 2018)

## Attendees
*   Italo Busi
*   Sergio Belotti
*   Carlo Perocchio
*   Gianmarco Bruno
*   Igor Bryskin
*   Yuji Tochio
  

## Agenda

1) Status update after IETF 101  
2) JSON code updates  
    2.1) I2RS Topology attributes  
    2.2) ODU2 and EPL Service Examples  
3) AOB  
  

## Meeting Notes

### 1) Status update after IETF 101

  
Minutes of the face-to-face meeting during IETF 101:  
[https://github.com/danielkinguk/transport-nbi/tree/master/Meetings/2018-03-17-23-IETF101](https://github.com/danielkinguk/transport-nbi/tree/master/Meetings/2018-03-17-23-IETF101)  
  
Need to assign some action points:  
      

#### 1.1) Review of OpenConfig model ([open issue#20](https://github.com/danielkinguk/transport-nbi/issues/20))

  
**Action assigned to Sergio**: Review in details the OpenConfig model to check if there is something which can be used by the TNBI DT or confirm that there is nothing that can be reused  
  

#### 1.2) Relationship with the TE Tutorial in TEAS ([open issue#19](https://github.com/danielkinguk/transport-nbi/issues/19))

  
**Action assigned to Italo and Sergio**: Review in details the two drafts to understand which text should be moved into the TE Tutorial and which text should be replaced with a reference to the TE Tutorial.  
  

#### 1.3) Multi-layer Modelling with ACTN ([open issue #28](https://github.com/danielkinguk/transport-nbi/issues/28))

  
The feedbacks is that it is possible that ODU and WDM networks are managed by different departments so the multi-layer issue #28 applies also within the Optical network.  
  
**Action (Italo): Ask operators in the DT to confirm this working assumption.**  
  

### 2) JSON code updates

  

#### 2.1) I2RS Topology attributes

  
The issue is more general and it is related to how to identify topology elements  
  
There are three proposals on the table to be evaluated/reconciled:  
  

*   [https://github.com/danielkinguk/transport-nbi/pull/10](https://github.com/danielkinguk/transport-nbi/pull/10)
    
*   [https://github.com/danielkinguk/transport-nbi/pull/24/commits/caf2a364209e5b52a641ed3be366baff8d9ab838](https://github.com/danielkinguk/transport-nbi/pull/24/commits/caf2a364209e5b52a641ed3be366baff8d9ab838)
    
*   [https://tools.ietf.org/html/draft-ietf-teas-te-topo-and-tunnel-modeling-01](https://tools.ietf.org/html/draft-ietf-teas-te-topo-and-tunnel-modeling-01)

  
**Action (Carlo/Gianmarco/Italo/Igor): work offline to evaluate/reconcile the proposals and develop a JSON example to be discussed by the DT**  
  
Initial call planned on Friday April 27, 2018 at 4:30pm CEST and 10:30am EDT  
  

#### 2.2) ODU2 and EPL Service Examples

  
[Pull Request #29](https://github.com/danielkinguk/transport-nbi/pull/29)  
  
Confirmed that hierarchical-link container should be empty in case of tunnel transit segments  
  
The hierarchical-link container should be under the tunnel rather than under the p2p-primary-path  
  
**Action (Italo): Raise an issue to TE tunnel model authors/contributors**  
  
The te-bandwidth information per path allows configuring protection paths with lower bandwidth. The tunnel te-bandwidth is assumed to be the bandwidth of a path unless the te-bandwidth of the path is not specified.  
  
This is not typical in transport network: it is possible to only specify the te-bandwdith information for the tunnel and no te-bandwidth infromation for the paths.  
  

### 3) AOB

  
The modelling of bidirectional tunnels/LSPs is still under discussion among TE Tunnel authors and contributions:  
  
[TE Tunnel Open Issue #25](https://github.com/ietf-mpls-yang/te/issues/25)  
  
It is not clear why the association container is needed since the association should be between LSPs and not between tunnels  
  
DT members are invited to join the discussion with TE tunnel authors/contributors on friday  
  

Note Takers
-----------

*   Italo Busi
