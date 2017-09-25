# Weekly Call (September 20, 2017)

## Attendees

* Italo Busi  
* Daniel King  
* Sergio Belotti  
* Carlo Perocchio  
* Dieter Beller  
* Gianmarco Bruno  
* Masanori Mihazawa  
* Oscar Dios Gonzalez  
* Young Lee  

## Agenda:

1) Use Case I-D  
2) Use Case 1 Analysis  
3) Use Case 3 Analysis  
4) AOB  

## Meeting Notes:

### 1) Use Case I-D

The document is ready to be uploaded on IETF and polled for CCAMP WG adoption  

**Actions: Dan to perform one last English review before submission**

### 2) Use Case 1 Analysis

Contribution from Gianmarco on how to fix the comments in JSON code to fit into the I-D width  
[https://github.com/danielkinguk/transport-nbi/pull/4](https://github.com/danielkinguk/transport-nbi/pull/4)  

The possibility to split long comments into multiple lines is useful.  

The tool that allows removing the comments before the JSON code validation is availble on Gianmarco GitHub:  
[https://github.com/GianmarcoBruno/json-yang/blob/master/scripts/Stripper.py](https://github.com/GianmarcoBruno/json-yang/blob/master/scripts/Stripper.py)  

Contribution from Ricard on JSON code automatically generated:  
[https://github.com/danielkinguk/transport-nbi/pull/5](https://github.com/danielkinguk/transport-nbi/pull/5)  

**Action (Gianmarco): check that the new JSON code fit into the I-D 72 characters width and it passes the YANG validation checks.**

### 3) Use Case 3 Analysis

Contribution from Haomian:  
[https://github.com/danielkinguk/transport-nbi/pull/6](https://github.com/danielkinguk/transport-nbi/pull/6)  

In order to allow the MDSC to stitch together the different topologies provided by the PNCs, the plug-id attribute, defined in TE Topology mode, is needed.  

There is some administrative burden to configure the plug-id. They are already described in RFC7926.  

The text "MDSC need to determine the domain sequence" in the process description seems too restrictive since in some cases MDSC may need to use Path Computation to get more information from the PNCs before determining the domain sequence.  

Another option is to rely on inter-domain discovery using e.g., the TTI.  

The DT will analyse both cases (configuration and auto-discovery) with the understanding that both cases rely on administrative task to be performed by means which are outside the scope of the DT.  

The abstraction level on the inter-domain links should be white (i.e, no abstraction) to allow the MDSC to control them. Also technology-specific information needs to be available on the inter-domain links.  

Review and comments to continue via mailing list and next DT calls.  

The pull request will be merged to take this document as the initial draft version for the DT to further work.  

**Action (Haomian): update the draft to address the comments raised during the call.**  

### 4) AOB

Next call is planned for next week (September 27, 2017) at 3pm CEST.  

## Note Takers

* Italo Busi  
* Daniel King  
