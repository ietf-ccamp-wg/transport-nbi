---
coding: utf-8

title: Transport Northbound Interface Applicability Statement

abbrev: Transport NBI Applicability-Statement
docname: draft-ietf-ccamp-transport-nbi-app-statement-16
workgroup: CCAMP Working Group
category: info
ipr: trust200902

stand_alone: yes
pi: [toc, sortrefs, symrefs, comments]

author:
  -
    name: Italo Busi
    role: editor
    org: Huawei
    email: italo.busi@huawei.com
  -
    name: Daniel King
    role: editor
    org: Old Dog Consulting
    email: daniel@olddog.co.uk
  -
    name: Haomian Zheng
    role: editor
    org: Huawei
    email: zhenghaomian@huawei.com
  -
    name: Yunbin Xu
    role: editor
    org: CAICT
    email: xuyunbin@ritt.cn

contributor:
  -
    name: Yang Zhao
    org: China Mobile
    email: zhaoyangyjy@chinamobile.com
  -
    name: Sergio Belotti
    org: Nokia
    email: sergio.belotti@nokia.com
  -
    name: Gianmarco Bruno
    org: Ericsson
    email: gianmarco.bruno@ericsson.com
  -
    name: Young Lee
    org: Sung Kyun Kwan University
    email: younglee.tx@gmail.com
  -
    name: Victor Lopez
    org: Nokia
    email: victor.lopez@nokia.com
  -
    name: Carlo Perocchio
    org: Ericsson
    email: carlo.perocchio@ericsson.com
  -
    name: Ricard Vilalta
    org: CTTC
    email: ricard.vilalta@cttc.es
  -
    name: Michael Scharf
    org: Hochschule Esslingen - University of Applied Sciences
    email: michael.scharf@hs-esslingen.de
  -
    name: Dieter Beller
    org: Nokia
    email: dieter.beller@nokia.com

normative:
  ITU-T_G.709:
    title: Interfaces for the optical transport network
    author:
      org: ITU-T Recommendation G.709
    date: March 2020
    seriesinfo: ITU-T G.709
  ITU-T_G.808.1:
    title: Generic protection switching - Linear trail and subnetwork protection
    author:
      org: International Telecommunication Union
    date: May 2014
    seriesinfo: ITU-T Recommendation G.808.1
  ITU-T_G.873.1:
    title: >
        Optical transport network (OTN): Linear protection
    author:
      org: International Telecommunication Union
    date: October 2017
    seriesinfo: ITU-T Recommendation G.873.1
  OTN-TOPO: I-D.ietf-ccamp-otn-topo-yang
  CLIENT-TOPO: I-D.ietf-ccamp-eth-client-te-topo-yang
  TE-TUNNEL: I-D.ietf-teas-yang-te
  PATH-COMPUTE: I-D.ietf-teas-yang-path-computation
  OTN-TUNNEL: I-D.ietf-ccamp-otn-tunnel-model
  CLIENT-SIGNAL: I-D.ietf-ccamp-client-signal-yang

informative:
  ACTN-YANG: I-D.ietf-teas-actn-yang
  ITU-T_X.733:
    title: >
        Information technology - 
        Open Systems Interconnection - 
        Systems Management: Alarm reporting function
    author:
      org: International Telecommunication Union
    date: February 1992
    seriesinfo: ITU-T Recommendation X.733
  ITU-T_X.734:
    title: >
        Information technology - 
        Open Systems Interconnection - 
        Systems Management: Event report management function
    author:
      org: International Telecommunication Union
    date: September 1992
    seriesinfo: ITU-T Recommendation X.734
  ONF_TR-527:
    title: Functional Requirements for Transport API
    author:
      org: Open Networking Foundation
    date: May 2014
    seriesinfo: ONF Technical Recommendation TR-527
  MEF55:
    title: >
        Lifecycle Service Orchestration (LSO): Reference Architecture and Framework
    author:
      org: MEF Forum
    date: March 2016
    seriesinfo: MEF 55
    target: https://www.mef.net/Assets/Technical_Specifications/PDF/MEF_55.pdf

--- abstract

   This document provides an analysis of the applicability of the YANG
   models defined by the IETF (in particular in the Traffic Engineering
   Architecture and Signaling (TEAS) and Common Control and Measurement
   Plane (CCAMP) working groups) to support ODU transit services,
   transparent client services, and Ethernet Private Line/Ethernet
   Virtual Private Line (EPL/EVPL) services over Optical Transport
   Network (OTN) in single and multi-domain network scenarios.

   This document also describes how existing YANG models can be used
   through several worked examples and JSON fragments.

--- middle

{: #introduction}

# Introduction

   Transport network domains, including Optical Transport Network (OTN)
   and Wavelength Division Multiplexing (WDM) networks are typically
   deployed based on a single vendor or a single technology platform.  
   They are often managed using proprietary interfaces to dedicated 
   Element Management Systems (EMS), Network Management Systems (NMS) and
   increasingly Software Defined Network (SDN) controllers.
   
   Support of packet connectivity services over a transport network
   domain is critical for a wide range of applications and services,
   including data center and LAN interconnects, Internet service
   backhauling, mobile backhaul and enterprise Carrier Ethernet
   services. An explicit goal of operators is to automate the setup of
   these connectivity services across multiple transport network
   domains, that may utilize different technologies.
   
   A well-defined common open interface to each domain controller or a
   management system is required for network operators to control multi-
   vendor and multi-domain networks and also enable coordination and
   automation of service provisioning.  This is facilitated by using
   standardized data models (e.g., YANG models), and an appropriate
   protocol (e.g., RESTCONF {{?RFC8040}}).
  
   This document examines the applicability of the YANG models defined
   by the IETF (in particular in the Traffic Engineering Architecture
   and Signaling (TEAS) and Common Control and Measurement Plane (CCAMP)
   working groups) to support OTN in a single and multi-domain network
   scenarios.

{: #scope}

## The Scope of this Document

   This document assumes a reference architecture, including interfaces,
   based on the Framework for Abstraction and Control of Traffic- 
   Engineered Networks (ACTN), defined in {{!RFC8453}}.
   
   The focus of this document is on the interface between the Multi
   Domain Service Coordinator (MDSC) and a Provisioning Network
   Controller (PNC), controlling a transport network domain, called
   MDSC-PNC Interface (MPI) in {{!RFC8453}}.
   
   It is worth noting that the same MPI analyzed in this document could
   be used between hierarchical MDSC controllers, as shown in Figure 4
   of {{!RFC8453}}.
   
   A detailed analysis of the interface between the Customer Network
   Controller (CNC) and the MDSC, called CNC-MDSC Interface (CMI), in
   {{!RFC8453}}, as well as the interface between service and network,
   orchestrators are outside the scope of this document.  However, when
   needed, this document describes some considerations and assumptions
   about the information that must be provided at these interfaces.
   The list of the IETF YANG models which apply to the ACTN MPI
   can be found in {{ACTN-YANG}}.

   The Functional Requirements for the transport API as described in the
   Optical Networking Foundation (ONF) document {{ONF_TR-527}} have been
   taken as input for defining the reference scenarios analyzed in this
   document.

   The analysis provided in this document confirms that the IETF YANG
   models defined in {{!RFC8453}}, {{!RFC8795}}, {{OTN-TOPO}}, {{CLIENT-TOPO}},
   {{TE-TUNNEL}}, {{PATH-COMPUTE}}, {{OTN-TUNNEL}}, and {{CLIENT-SIGNAL}} can be
   used together to control a multi-domain OTN network to support
   different types of multi-domain services, such as Optical Data Unit 
   (ODU) transit services, Transparent client services and EPL/EVPL 
   Ethernet Private Line/Ethernet Virtual Private Line (EPL/EVPL)    
   services, over a multi-domain OTN connection, also satisfying 
   the requirements in {{ONF_TR-527}}.

{: #terminology}

# Terminology

Domain:

> A domain, as defined in {{!RFC4655}}, is "any collection of
network elements within a common sphere of address management or
path computation responsibility".  Specifically, within this
document, we mean a part of an operator's network under
common management (i.e., under shared operational management using
the same instances of a tool and the same policies).  Network
elements are often grouped into domains based on technologies,
vendor profiles, or geographic proximity.

CNC:

> Customer Network Controller

Connection:

> The data plane configuration of an LSP: within this
document it is typically an ODU LSP.  An end-to-end connection/LSP
represents an entire connection between the connection
node end-points.  A connection/LSP segment represents a portion of
the end-to-end connection.

Connectivity Service:

> A connectivity service, in the context of this document, can be 
considered as a connection between customer sites, across the network
operator's network {{?RFC8309}}.

E-LINE:

> Ethernet Line

EPL:

> Ethernet Private Line

EVPL:

> Ethernet Virtual Private Line

ILL:

> Inter-Layer Lock

Link:

> It is used to represent the adjacency between two nodes.  
The term physical link represents a link between two physical
nodes. The term OTN link represents a link between two OTN nodes. 

LSP:

> Label Switched Path

LTP:

> Link Termination Point

MDSC:

> Multi-Domain Service Coordinator

Network Configuration:

> As described in {{?RFC8309}} it describes the
instructions provided to a controller on how to configure parts of a
network.

ODU:

> Optical Channel Data Unit

OTU:

> Optical Channel Transport Unit

OTN:

> Optical Transport Network

PNC:

> Provisioning Network Controller

Protection Switching:

> Protection switching, as defined in {{ITU-T_G.808.1}}
and {{!RFC4427}}, provides the capability to switch the traffic
in case of network failures over pre-allocated networks resources.
Typically linear protection methods would be used and configured to
operate as 1+1 unidirectional, 1+1 bidirectional or 1:n
bidirectional. This ensures fast and simple service survivability.

Protection Transport Entity/LSP:

> A protection transport entity/LSP,
as defined in {{ITU-T_G.808.1}} and {{!RFC4427}}, represents the path
where the "normal" user traffic is transported during protection
switching events (e.g., when the working transport entity/LSP
fails).

Restoration:

> Restoration methods, as defined in {{!RFC4427}}, provide
the capability to reroute and restore traffic around network
failures without the necessity to allocate network resources as
required for dedicated 1+1 protection schemes. On the other hand,
restoration times are typically longer than protection switching
times.

Service Model:

> As described in {{?RFC8309}} it describes a service and
the parameters of the service in a portable way that can be used
uniformly and independent of the equipment and operating
environment.

TE Link:

> As defined in {{!RFC8795}}, is an element of a TE topology,
presented as an edge on TE graph.

TE Tunnel:

> As defined in {{TE-TUNNEL}}, is a connection-oriented
service provided by a layered network of delivery of a client's data
between source and destination tunnel termination points.

TE Tunnel Segment:

> As defined in {{TE-TUNNEL}}, is a part of a
multi-domain TE tunnel that spans.

TE Tunnel Hand-off:

> Is an access or inter-domain LTP by
which a multi-domain TE tunnel enters or exits a given network
domain.

TPN:

> Tributary Port Number

TTP:

> Tunnel Termination Point

Termination and Adaptation:

> It represents the termination of a
server-layer connection at the node edge-point and the
adaptation/mapping of the client layer traffic over the terminated
server-layer connection.

Transparent Client:

> As defined in {{CLIENT-SIGNAL}}, it represents a
client-layer signal, such as Ethernet physical interfaces, FC, STM-
n, that cannot be switched but only mapped over a server-layer TE
Tunnel.

Working Transport Entity/LSP:

> A working transport entity/LSP, as
defined in {{ITU-T_G.808.1}} and {{!RFC4427}}, represents the path where
the "normal" user traffic is transported.

UNI:

> User Network Interface

{: #conventions}

# Conventions Used in this Document

{: #process-convention}

## Topology and Traffic Flow Processing

   The traffic flow between different nodes is specified as an ordered
   list of nodes, separated with commas, indicating within the brackets
   the processing within each node:

~~~~
      <node> [<processing>]{, <node> [<processing>]}
~~~~

   The order represents the order of traffic flow being forwarded
   through the network.

   The \<processing> represents the type of processing performed by the
   node, which can be just switching at a given layer
   "(switching-layer)" or it can also include an adaptation of a client
   layer into a server layer: "(client-layer) -> server-layer" or
   "client-layer -> (server-layer)", where the round brackets are used
   to represent at which layer (client layer or server layer) the node
   is switching.

   For example, the following traffic flow:

~~~~
      R1 [(PKT) -> ODU2], S3 [(ODU2)], S5 [(ODU2)], S6 [(ODU2)],
      R3 [ODU2 -> (PKT)]
~~~~

   Node R1 is switching at the packet (PKT) layer and mapping packets
   into an ODU2 before transmission to node S3. Nodes S3, S5 and S6,
   are switching at the ODU2 layer: S3 sends the ODU2 traffic to S5,
   which then sends it to S6, which finally sends to R3. Node R3
   terminates the ODU2 from S6 before switching at the packet (PKT)
   layer.

   The paths of working and protection transport entities are specified
   as an ordered list of nodes, separated with commas:

~~~~
      <node> {, <node>}
~~~~

   The order represents the order of traffic flow being forwarded
   through the network in the forward direction. In the case of
   bidirectional paths, the forward and backward directions are
   selected arbitrarily, but the convention is consistent between
   working/protection path pairs, as well as across multiple domains.
   
   The use of curly brackets denotes multiple nodes in a list. 

{: #scenarios}

# Scenarios Description

{: #reference-network}

## Reference Network

   The physical topology of the reference network is shown in 
   {{fig-reference-network}}.
   It represents an OTN network composed of three transport network
   domains that provide connectivity services to an IP customer
   network through nine access links:

~~~~

               ........................
   .........   :                      :
           :   :   Network domain 1   :   .............
   Customer:   :                      :   :           :
    domain :   :     S1 -------+      :   :  Network  :
           :   :    /           \     :   :  domain 3 :   ..........
       R1 ------- S3 ----- S4    \    :   :           :   :
           :   :    \        \    S2 --------+        :   :Customer
           :   :     \        \    |  :   :   \       :   : domain
           :   :      S5       \   |  :   :    \      :   :
       R2 ------+    /  \       \  |  :   :    S31 --------- R5
           :   : \  /    \       \ |  :   :   /   \   :   :
       R3 ------- S6 ---- S7 ---- S8 ------ S32   S33 ------ R6
           :   : /        |       |   :   : / \   /   :   :.......
       R4 ------+         |       |   :   :/   S34    :          :
           :   :..........|.......|...:   /    /      :          :
   ........:              |       |      /:.../.......:          :
                          |       |     /    /                   :
               ...........|.......|..../..../...                 :
               :          |       |   /    /   :    ..............
               : Network  |       |  /    /    :    :
               : domain 2 |       | /    /     :    :Customer
               :         S11 ---- S12   /      :    : domain
               :        /          | \ /       :    :
               :     S13     S14   | S15 ------------- R7
               :     |  \   /   \  |    \      :    :
               :     |   S16     \ |     \     :    :
               :     |  /         S17 -- S18 --------- R8
               :     | /             \   /     :    :
               :    S19 ---- S20 ---- S21 ------------ R9
               :                               :    :
               :...............................:    :.............

~~~~
{: #fig-reference-network title="Reference network"}

   This document assumes that all the Si transport network switching
   nodes are capable of switching in the electrical domain (ODU
   switching) moreover, all the Si-Sj OTN links within the
   transport network (intra-domain or inter-domain) are 100G links,
   while the access Ri-Sj links are 10G links.

   This document also assumes that within the transport network, the
   physical/optical connections supporting the Si-Sj OTN links (up to
   the OTU4 trail), are pre-provisioned using mechanisms that are
   outside the scope of this document and are not exposed at the MPIs
   to the MDSC.

   Different transmission technologies can be used on the access links
   (e.g., Ethernet, Synchronous Transport Module (STM) and OTU).
   {{service-description}} provides more details
   about the different assumptions on the access links for different
   types of connectivity services, and {{multi-function-access}} 
   describes the control of access links that can support different technology
   configurations (e.g., STM-64, 10GE or OTU2) depending on the type of
   service being configured (multi-function access links).

   To carry client signals (e.g., Ethernet or STM-N) over OTN, some ODU
   termination and adaptation resources need to be available on the
   physical edge nodes (e.g., node S3 and S18). The location of these
   resources within the physical node is implementation-specific and
   outside the scope of standardization. This document assumes that
   these termination and adaptation resources are located on the
   physical interfaces of the edge nodes terminating the access links.
   In other words, each physical access link has a set of dedicated ODU
   termination and adaptation resources.

   The transport network control architecture,
   shown in {{fig-control-hierarchy}},
   follows the ACTN architecture as defined in the ACTN framework
   document {{!RFC8453}}, and uses the same functional components:

~~~~

                           --------------
                          |              |
                          |     CNC      |
                          |              |
                           --------------
                                 |
             ....................|....................... CMI
                                 |
                          ----------------
                         |                |
                         |      MDSC      |
                         |                |
                          ----------------
                            /   |    \
                           /    |     \
            ............../.....|......\................ MPIs
                         /      |       \
                        /   ----------   \
                       /   |   PNC2   |   \
                      /     ----------     \
             ----------         |           \
            |   PNC1   |      -----          \
             ----------     (       )      ----------
                 |         (         )    |   PNC3   |
               -----      (  Network  )    ----------
             (       )    (  Domain 2 )        |
            (         )    (         )       -----
           (  Network  )    (       )      (       )
           (  Domain 1 )      -----       (         )
            (         )                  (  Network  )
             (       )                   (  Domain 3 )
               -----                      (         )
                                           (       )
                                             -----

~~~~
{: #fig-control-hierarchy title="Controlling Hierarchies"}

   The NEs within network domains 1, 2 and 3 of {{fig-reference-network}} are
   controlled, respectively, by PNC1, PNC2 and PNC3 of {{fig-control-hierarchy}}. The
   MDSC controls the end-to-end network through the MPIs toward the
   underlying PNCs.

   The ACTN framework facilitates separating the network and
   service control from the underlying technology. It helps the
   customer to define the network as desired by business needs. The CMI
   is defined to keep a minimal level of dependency (or no dependency
   at all) from the underlying network technologies. The MPI instead
   requires some specialization according to the domain technology.

   The control interfaces within the scope of this document are the
   three MPIs, as shown in {{fig-control-hierarchy}}.

   The split of functionality at the MPI in the ACTN architecture
   between the MDSC and the PNCs, is equivalent to separation functionality assumed in
   the ONF T-API interface, as described in the ONF T-API multi-domain
   use cases {{ONF_TR-527}}. Furthermore, this functional separation is
   similarly defined in the MEF PRESTO interface between the Service
   Orchestration Functionality (SOF) and the Infrastructure Control and
   Management (ICM) in the MEF LSO Architecture {{MEF55}}.

   This document does not make any assumption about the control
   architecture of the customer IP network: in line with {{!RFC8453}}, the
   CNC is just a functional component within the customer control
   architecture which is capable of requesting connectivity services on
   demand between IP routers at the CMI.

   The CNC can request connectivity services between IP routers which
   can be attached to different transport network domains (e.g.,
   between R1 and R8 in {{fig-reference-network}}) or to the same transport network
   domain (e.g., between R1 and R3 in {{fig-reference-network}}). Since the CNC is not
   aware of the transport network controller hierarchy, the mechanisms
   used by the CNC to request connectivity services at the CMI is also
   unaware whether the requested service spans a single-domain or
   multi-domains.

   It is assumed that the CMI allows the CNC to provide all the
   necessary information needed by the MDSC to understand the
   connectivity service request and to determine the network
   configurations to be requested, at the MPIs, to its underlying PNCs
   to support the requested connectivity service.

   The MDSC, after having received a single-domain service request from
   the CNC at the CMI (e.g., between R1 and R3 in {{fig-reference-network}}), can follow
   the same procedures, described above for the multi-domain service,
   and decide the network configuration to request only at the MPI of
   the PNC controlling that domain (e.g., MPI1 of PNC1 in {{fig-control-hierarchy}}).

{: #topology-description}

## Topology Abstractions

   Abstraction provides a selective method for representing
   connectivity information within a domain. There are multiple methods
   to abstract a network topology. This document assumes the
   abstraction method defined in {{!RFC7926}}:

>   Abstraction is the process of applying policy to the available TE
>   information within a domain, to produce selective information that
>   represents the potential ability to connect across the domain.  Thus,
>   abstraction does not necessarily offer all possible connectivity
>   options, but it presents a general view of potential connectivity
>   according to the policies that determine how the domain's
>   administrator wants to allow the domain resources to be used.

   {{!RFC8453}} Provides the context of topology abstraction in the ACTN
   architecture and discusses a few alternatives for the abstraction
   methods for both packet and optical networks. This is an important
   consideration since the choice of the abstraction method impacts
   protocol design and the information it carries.  According to
   {{!RFC8453}}, there are three types of topologies:

   -  White topology: This is a case where the PNC provides the actual
      network topology to the MDSC without any hiding or filtering. In
      this case, the MDSC has full knowledge of the underlying
      network topology;

   -  Black topology: The entire domain network is abstracted as a
      single virtual node with access links and inter-domain links
      without disclosing any node internal connectivity information;

   -  Grey topology: This abstraction level is between black topology
      and white topology from a granularity point of view.

   Each PNC should provide the MDSC with a network topology abstraction
   hiding the internal details of the physical domain network topology
   controlled by the PNC. As described in section 3 of {{!RFC8453}}, the
   level of abstraction provided by each PNC is based on the PNC
   configuration parameters, and it is independent of the abstractions
   provided by other PNCs. Therefore, it is possible that different
   PNCs provide different topology abstractions. The MDSC can
   operate on each MPI abstract topology regardless of, and
   independently from, the type of abstraction provided by its
   underlying PNC.

   For analyzing how the MDSC can operate on an abstract topology
   provided by several PNCs that independently applied different
   abstraction policies and therefore provided different types of
   abstract topologies, the following assumptions are made for the
   reference network in {{fig-reference-network}}:

   -  PNC1 and PNC2 provide black topology abstractions which expose at
      MPI1, and MPI2 respectively, a single virtual node (representing
      the whole network domain 1, and domain 2, respectively).

   -  PNC3 provides a white topology abstraction which exposes at MPI3
      all the physical nodes and links within network domain 3.

   The MDSC should be capable of stitching together the abstracted
   topologies provided by each PNC to build its view of the multi-
   domain network topology. This topology knowledge may require proper
   oversight, including the application of local policy, configuration
   methods, and the application of a trust model. Methods of how to
   manage these aspects are out of the scope for this document, but
   recommendations are provided in the Security section of this
   document.

   The MDSC can also provide topology abstraction of its view of the
   multi-domain network topology at its CMIs depending on the
   customers' needs and policies: it can provide different 
   topology abstractions at different CMIs. Analyzing the topology
   abstractions provided by the MDSC to its CMIs is outside the scope
   of this document.

{: #service-description}

## Service Configuration

   In the following scenarios, it is assumed that the CNC is capable of
   requesting connectivity services from the MDSC, for example, to
   interconnect IP routers.

   The type of connectivity services depends on the type of physical
   links (e.g. OTN link, ETH link or SDH link) between the routers and
   transport network.

   The packet processing inside IP routers, including packet
   encapsulation and decapsulation, Ri (PKT -> foo) and Rj (foo ->
   PKT), are assumed to be performed by means that are not under the
   control of, and not visible to, the MDSC or the PNCs. Therefore,
   these mechanisms are outside the scope of this document.

{: #odu-description}

### ODU Transit

   The physical links interconnecting the IP routers and the transport
   network can be 10G OTN links.

   In this case, it is assumed that the physical/optical
   interconnections below the ODU layer (up to the OTU2 trail) are
   pre-provisioned using mechanisms which are outside the scope of this
   document and not exposed at the MPIs between the PNCs and the MDSC.

   For simplicity of the description, it is also assumed that these
   interfaces are not channelized (i.e., they can only support one
   ODU2).

   When a 10Gb IP connectivity service between R1 and R8 is needed, an ODU2 end-to-end
   connection needs to be created, passing through transport network
   nodes S3, S1, S2, S31, S33, S34, S15 and S18, which belong to
   different PNC domains (multi-domain service request):

~~~~
      R1 [(PKT) -> ODU2], S3 [(ODU2]), S1 [(ODU2]), S2 [(ODU2]),
      S31 [(ODU2)], S33 [(ODU2)], S34 [(ODU2)],
      S15 [(ODU2)], S18 [(ODU2)], R8 [ODU2 -> (PKT)]
~~~~

   The MDSC receives, at the CMI, the request to create an ODU2 transit
   service between the access links on S3 and S18, which belong to
   different PNC domains (multi-domain service request). The MDSC also
   determines the network configuration requests to be sent to its
   underlying PNCs, at the MPIs, to coordinate the setup of a multi-
   domain ODU2 connection segment between the access links on S3 and
   S18.

   When a 10Gb IP connectivity service between R1 and R3 is needed, an ODU2 end-to-end
   connection needs to be created, passing through transport network
   nodes S3, S5 and S6 which belong to the same PNC domain (single-
   domain service request):

~~~~
      R1 [(PKT) -> ODU2], S3 [(ODU2)], S5 [(ODU2)], S6 [(ODU2)],
      R3 [ODU2 -> (PKT)]
~~~~

   As described in {{reference-network}},
   the mechanisms, used by the CNC at the
   CMI, are independent of whether the service request is single-domain
   service or multi-domain.

   The MDSC can figure out that it needs to setup an ODU2 transit
   service between the access links on S3 and S6, which belong to the
   same PNC domain (single-domain service request) and it decides the
   proper network configuration to request PNC1.

{: #client-description}

### Transparent Client Services

   {{ITU-T_G.709}} defines mappings of different Transparent Client
   layers into ODU. Most of them are used to provide Private Line
   services over an OTN transport network supporting a variety of types
   of physical access links (e.g., Ethernet, SDH STM-N, Fibre Channel,
   InfiniBand, etc.) interconnect the IP routers and the transport
   network.

   When a 10Gb IP connectivity service between R1 and R8 is needed, using, for example
   SDH physical links between the IP routers and the transport network,
   an STM-64 Private Line service needs to be created, supported by a
   ODU2 end-to-end connection, between transport network nodes S3 and
   S18, passing through transport network nodes S1, S2, S31, S33, S34
   and S15, which belong to different PNC domains (multi-domain service
   request):

~~~~
      R1 [(PKT) -> STM-64], S3 [STM-64 -> (ODU2)], S1 [(ODU2)],
      S2 [(ODU2)], S31 [(ODU2)], S33 [(ODU2)], S34[(ODU2)],
      S15 [(ODU2)], S18 [(ODU2) -> STM-64], R8 [STM-64 -> (PKT)]
~~~~

   As described ({{reference-network}}) the CNC provides the essential
   information to permit the MDSC to compute which type of service is
   needed, in this case, an STM-64 Private Line Service between the
   access links on S3 and S8, and it also decides the network
   configurations, including the configuration of the adaptation
   functions inside these edge nodes, such as S3 \[STM-64 -> (ODU2)] and
   S18 \[(ODU2) -> STM-64].

   When a 10Gb IP connectivity service between R1 and R3 is needed, an STM-64 Private
   Line service needs to be created between R1 and R3 (single-domain
   service request):

      R1 [(PKT) -> STM-64], S3[STM-64 -> (ODU2)], S5 [(ODU2)],
      S6 [(ODU2) -> STM-64], R3[STM-64 -> (PKT)]

   As described in {{reference-network}}, the mechanisms, used by the CNC at the
   CMI, are independent of whether the service request is single-domain
   service or multi-domain.

   Based on the assumption above, in this case, the MDSC can figure out
   that it needs to setup an STM-64 Private Line service between the
   access links on S3 and S6, which belong to the same PNC domain
   (single-domain service request), and it decides the proper network
   configuration to request PNC1.

{: #evpl-description}

### EPL and EVPL over ODU

   The physical links interconnecting the IP routers and the transport
   network can be 10G Ethernet physical links (10GE).

   In this case, it is assumed that the Ethernet physical interfaces
   (up to the MAC layer) are pre-provisioned using mechanisms which are
   outside the scope of this document and not exposed at the MPIs
   between the PNCs and the MDSC.

   When a 10Gb IP connectivity service between R1 and R8 is needed, an EPL
   service needs to be created, supported by an ODU2 end-to-end
   connection, between transport network nodes S3 and S18, passing
   through transport network nodes S1, S2, S31, S33, S34 and S15, which
   belong to different PNC domains (multi-domain service request):

~~~~
      R1 [(PKT) -> ETH], S3 [ETH -> (ODU2)], S1 [(ODU2)],
      S2 [(ODU2)], S31 [(ODU2)), S33 [(ODU2)], S34 [(ODU2)],
      S15 [(ODU2)], S18 [(ODU2) -> ETH], R8 [ETH -> (PKT)]
~~~~

   The MDSC receives, at the CMI, the request to create an EPL service
   between the access links on S3 and S18, which belong to different
   PNC domains (multi-domain service request). The MDSC determines the
   network configurations to request, at the MPIs, to its underlying
   PNCs, to coordinate the setup of an end-to-end ODU2 connection
   between the nodes S3 and S8, including the configuration of the
   adaptation functions inside these edge nodes, such as S3 \[ETH ->
   (ODU2)] and S18 \[(ODU2) -> ETH].

   When a 10Gb IP connection between R1 and R2 is needed, an EPL service
   needs to be created, supported by an ODU2 end-to-end connection
   between transport network nodes S3 and S6, passing through the
   transport network node S5, which belongs to the same PNC domain
   (single-domain service request):

~~~~
      R1 [(PKT) -> ETH], S3 [ETH -> (PKT)] S5 [(ODU2)],
      S6 [(ODU2) -> ETH], R2 [ETH -> (PKT)]
~~~~

   As described in {{reference-network}}, the mechanisms used by the CNC at the
   CMI are independent of whether the service request is single-domain
   service or multi-domain.

   Based on the assumption above, in this case, the MDSC can figure out
   that it needs to setup an EPL service between the access links on S3
   and S6, that belongs to the same PNC domain (single-domain service
   request) and it decides the proper network configuration to request
   PNC1.

   When two 1Gb IP links between R1 to R2 and between R1 and R8 are
   needed, two EVPL services need to be created, supported by two ODU0
   end-to-end connections:

~~~~
      R1 [(PKT) -> VLAN], S3 [VLAN -> (ODU0)], S5 [(ODU0)],
      S6 [(ODU0) -> VLAN], R2 [VLAN -> (PKT)]

      R1 [(PKT) -> VLAN], S3[VLAN -> (ODU0)], S1 [(ODU0)],
      S2 [(ODU0)], S31 [(ODU0)], S33 [(ODU0)], S34 [(ODU0)],
      S15 [(ODU0)], S18 [(ODU0) -> VLAN], R8[VLAN -> (PKT)]
~~~~

   It is worth noting that the first EVPL service is required between
   access links which belong to the same PNC domain (single-domain
   service request) while the second EVPL service is required between
   access links which belong to different PNC domains (multi-domain
   service request).

   Since the two EVPL services share the same Ethernet physical
   link between R1 and S3, different VLAN IDs are associated with
   different EVPL services: for example, VLAN IDs 10 and 20
   respectively.

   The CNC sends a
   request to the MDSC, at the CMI, to set up these EVPL services. The
   MDSC will determine the network configurations to request to the
   underlying PNCs.

{: #multi-function-access}

## Multi-Function Access Links

   Some physical links interconnecting the IP routers and the transport
   network can be configured in different modes, e.g., as OTU2 trail or
   STM-64 or 10GE physical links.

   This configuration can be pre-provisioned by means which are outside
   the scope of this document. In this case, these links will appear at
   the MPI as links supporting only one mode (depending on how the link
   has been pre-provisioned) and will be controlled at the MPI as
   discussed in {{service-description}}:
   for example, a 10G multi-function access
   link can be pre-provisioned as an OTU2 trail ({{odu-description}}), a 10GE
   physical link ({{evpl-description}}) or an STM-64 physical link
   ({{client-description}}).

   It is also possible not to configure these links a-priori and let
   the MDSC (or, in case of a single-domain service request, the PNC)
   decide how to configure these links, based on the service
   configuration.

   For example, if the physical link between R1 and S3 is a
   multi-functional access link while the physical links between R4 and
   S6 and between R8 and S18 are STM-64 and 10GE physical links
   respectively, it is possible to configure either an STM-64 Private
   Line service between R1 and R4 or an EPL service between R1 and R8.

   The traffic flow between R1 and R4 can be summarized as:

~~~~
      R1 [(PKT) -> STM-64], S3 [STM-64 -> (ODU2)], S5 [(ODU2)],
      S6 [(ODU2) -> STM-64], R4 [STM-64 -> (PKT)]
~~~~

   The traffic flow between R1 and R8 can be summarized as:

~~~~
      R1 [(PKT) -> ETH], S3 [ETH -> (ODU2)], S1 [(ODU2)],
      S2 [(ODU2)], S31 [(ODU2)), S33 [(ODU2)], S34 [(ODU2)],
      S15 [(ODU2)], S18 [(ODU2) -> ETH], R8 [ETH -> (PKT)]
~~~~

   The CNC is capable of requesting, via the CMI, the setup of either an
   STM-64 Private Line service, between R1 and R4, or an EPL service,
   between R1 and R8.

   The MDSC, based on the service being requested, decides the network
   configurations to request, at the MPIs, to its underlying PNCs, to
   coordinate the setup of an end-to-end ODU2 connection, either
   between nodes S3 and S6, or between nodes S3 and S18, including the
   configuration of the adaptation functions on these edge nodes, and
   in particularly whether the multi-function access link between R1 and
   S3 should operate as an STM-64 or as a 10GE physical link.

   Assumptions used in this example, as well as the service scenarios
   of {{service-description}}, include:

   -  the R1-S3 and R8-S18 access links will be multi-function access
      links, which can be configured as an OTU2 trail or as an STM-64
      or a 10GE physical link;

   -  the R3-S6 access link will be a multi-function access link which
      can be configured as an OTU2 trail or as an STM-64 physical link;

   -  the R4-S6 access link is pre-provisioned as an STM-64 physical
      link;

   -  all the other access links (and, in particular, the R2-S6 access
      links) are pre-provisioned as 10GE physical links, up to the MAC
      layer.

{: #protection-description}

## Protection and Restoration Configuration

   As described in {{!RFC4427}}, recovery can be performed by either
   protection switching or restoration mechanisms. This section
   describes only services which are protected with linear protection,
   considering both end-to-end and segment protection, as defined in
   {{ITU-T_G.808.1}} and {{!RFC4427}}. The description of services using
   dynamic restoration is outside the scope of this document.

   The MDSC needs to be capable of determining the network
   configurations to request different PNCs to coordinate the
   protection switching configuration to support protected connectivity
   services described in {{service-description}}.

   In the service examples described in {{service-description}}, switching within
   the transport network domain is only performed at the OTN ODU layer.
   Therefore, it is also assumed that protection switching within the
   transport network also occurs at the OTN ODU layer, using the
   mechanisms defined in {{ITU-T_G.873.1}}.

{: #linear-protection-description}

### Linear Protection (End-to-End)

   To protect the connectivity services described in {{service-description}} from
   failures within the OTN multi-domain transport network, the MDSC can
   decide to request its underlying PNCs to configure ODU2 linear
   protection between the transport network edge nodes (e.g., nodes S3
   and S18 for the services setup between R1 and R8).

   It is assumed that the OTN linear protection is configured as 1+1
   unidirectional protection switching type according to the definition
   in {{ITU-T_G.808.1}} and {{ITU-T_G.873.1}}, as well as in {{!RFC4427}}.

   In these scenarios, a working transport entity and a protection
   transport entity, as defined in {{ITU-T_G.808.1}}, (or a working LSP
   and a protection LSP, as defined in {{!RFC4427}}) should be configured
   in the data plane.

   Two cases can be considered:

   -  In one case, the working and protection transport entities pass
      through the same PNC domains:

~~~~
         Working transport entity:     S3, S1, S2,
                                       S31, S33, S34,
                                       S15, S18

         Protection transport entity:  S3, S4, S8,
                                       S32,
                                       S12, S17, S18
~~~~

   -  In another case, the working and protection transport entities
      can pass through different PNC domains:

~~~~
         Working transport entity:     S3, S5, S7,
                                       S11, S12, S17, S18

         Protection transport entity:  S3, S1, S2,
                                       S31, S33, S34,
                                       S15, S18
~~~~

   The PNCs should be capable of reporting to the MDSC which, is the
   active transport entity, as defined in {{ITU-T_G.808.1}}, in the data
   plane.

   Given the fast dynamic of protection switching operations in the
   data plane (e.g., 50ms switching time), this reporting is not
   expected to be in real-time.

   It is also worth noting that with unidirectional protection
   switching, e.g., 1+1 unidirectional protection switching, the active
   transport entity may be different in the two directions.

{: #segmented-protection-description}

### Segmented Protection

   To protect the connectivity services defined in {{service-description}} from
   failures within the OTN multi-domain transport network, the MDSC can
   decide to request its underlying PNCs to configure ODU2 linear
   protection between the edge nodes of each domain.

   For example, the MDSC can request PNC1 to configure linear protection
   between its edge nodes S3 and S2:

~~~~
      Working transport entity:     S3, S1, S2

      Protection transport entity:  S3, S4, S8, S2
~~~~

     MDSC can also request PNC2 to configure linear protection between
     its edge nodes S15 and S18:

~~~~
      Working transport entity:     S15, S18

      Protection transport entity:  S15, S12, S17, S18
~~~~

   MDSC can also request PNC3 to configure linear protection between
   its edge nodes S31 and S34:

~~~~
      Working transport entity:     S31, S33, S34

      Protection transport entity:  S31, S32, S34
~~~~

{: #notification-description}

## Event Notifications and Alarms

   To realize the three functions of topology update, service update,
   and restoration, the following notification types need to be
   supported:

   1. Object create

   2. Object delete

   3. Object state change

   4. Alarm

   There are three types of topology abstraction types defined in
   {{topology-description}}, and the notifications should also be abstracted. The
   PNC and MDSC should coordinate together to determine the
   notification policy. This will include information such as when an
   intra-domain alarm occurred. The PNC may not report the alarm, but
   it should provide notification of the service state change to the
   MDSC.

   Detailed analysis and methods of how event alarms are triggered, managed and
   propagated are outside the scope of this document.

## Path Computation with Constraints

   It is possible to define constraints to be taken into account during
   path computation procedures (e.g., Include Route Object (IRO) and Exclude Route Object (XRO) {{!RFC5521}}).

   For example, the CNC can request, at the CMI, an ODU transit
   service, as described in {{odu-description}}, between R1 and R8 with the
   constraint to pass through the link from S2 to S31 (IRO), such that
   a qualified path could be:

~~~~
      R1 [(PKT) -> ODU2], S3 [(ODU2]), S1 [(ODU2]), S2 [(ODU2]),
      S31 [(ODU2)], S33 [(ODU2)], S34 [(ODU2)],
      S15 [(ODU2)], S18 [(ODU2)], R8 [ODU2 -> (PKT)]
~~~~

   If the CNC instead requested to pass through the link from S8 to
   S12, then the above path would not be qualified, while the following
   would be:

~~~~
      R1 [(PKT) -> ODU2], S3[(ODU2]), S1 [(ODU2]), S2[(ODU2]),
      S8 [(ODU2]), S12[(ODU2]), S15 [(ODU2]), S18[(ODU2]), R8 [ODU2 ->
      (PKT)]
~~~~

   The mechanisms used by the CNC to provide path constraints at the
   CMI, are outside the scope of this document. It is assumed that the
   MDSC can satisfy these constraints and take them into account in its
   path computation procedures (which would decide at least which
   domains and inter-domain links) and in the path computation
   constraints to provide to its underlying PNCs, to be taken into
   account in the path computation procedures implemented by the PNCs
   (with a more detailed view of topology).

   Further detailed analysis is outside the scope of this document.

{: #analysis}

# YANG Model Analysis

   This section analyses how the IETF YANG models can be used at the
   MPIs, between the MDSC and the PNCs, to support the scenarios
   described in {{scenarios}}.

   The YANG models described in {{ACTN-YANG}} are assumed to be used at
   the MPI.

   {{topology-analysis}} describes the different topology abstractions provided
   to the MDSC by each PNC via its own MPI.

  {{service-analysis}} describes how the MDSC can request different PNCs, via
  their own MPIs, the network configuration needed to setup the
  different services described in {{service-description}}.

  {{protection-analysis}} describes how the protection scenarios can be deployed,
  including end-to-end protection and segment protection, for both
  intra-domain and inter-domain scenarios.

{: #topology-analysis}

## YANG Models for Topology Abstraction

   This section analyses how each PNC can report its respective
   abstract topology to the MDSC, as described in {{topology-description}}, using
   the Topology YANG models, defined in {{!RFC8345}}, with the TE Topology
   YANG augmentations, provided in {{!RFC8795}}, and the OTN
   technology-specific YANG augmentations, defined in {{OTN-TOPO}} or the
   Ethernet client technology-specific YANG augmentations, defined in
   {{CLIENT-TOPO}}.

   As described in {{reference-network}}, the OTU4 trails on inter-domain and
   intra-domain physical links are pre-provisioned and, therefore, not
   exposed at the MPIs. Only the TE Links they support can be exposed
   at the MPI, depending on the topology abstraction performed by the
   PNC.

   The access links can be multi-function access links, as described in
   {{multi-function-access}}.

   As described in {{reference-network}}, each physical access link has a
   dedicated set of ODU termination and adaptation resources.

   The {{OTN-TOPO}} model allows reporting within the OTN abstract
   topology also the access links which are capable of supporting the
   transparent client layers, defined in {{client-description}} and in
   {{CLIENT-SIGNAL}}. These links can also be multi-function access links
   that can be configured as transparent client physical links (e.g.,
   STM-64 physical link) or as an OTUk trail.

   In order to support the EPL and EVPL services, described in
   {{evpl-description}},
   the access links, which are capable of being
   configured as Ethernet physical links, are reported by each PNC
   within its respective Ethernet abstract topology, using the Topology
   YANG models, defined in {{!RFC8345}}, with the TE Topology YANG
   augmentations, defined in {{!RFC8795}}, and the Ethernet client
   technology-specific YANG augmentations, defined in {{CLIENT-TOPO}}.
   These links can also be multi-function access links that can be
   configured as an Ethernet physical link, an OTUk trail, or as a
   transparent client physical links (e.g., STM-64 physical link). In
   this case, these physical access links are represented in both the
   OTN and Ethernet abstract topologies.

   The PNC reports the capabilities of the access or inter-domain link
   ends it can control. It is the MDSC responsibility to request
   configuration of these links matching the capabilities of both link
   ends.

   It is worth noting that in the network scenarios analyzed in this
   document (where switching is performed only at the ODU layer), the
   Ethernet abstract topologies reported by the PNCs describe only the
   Ethernet client access links: no Ethernet TE switching capabilities
   are reported in these Ethernet abstract topologies, to report that
   the underlying network domain is not capable of supporting Ethernet TE
   Tunnels/LSPs.

{: #domain1-topo}

### Domain 1 Black Topology Abstraction

   PNC1 provides the required black topology abstraction, as described
   in {{topology-description}}. It exposes at MPI1 to the MDSC, two TE Topology
   instances with only one TE node each.

   The first TE Topology instance reports the domain 1 OTN abstract
   topology view (MPI1 OTN Topology), using the OTN technology-specific
   augmentations {{OTN-TOPO}}, with only one abstract TE node (i.e., AN1)
   moreover, only inter-domain and access abstract TE links (which
   represent the inter-domain physical links and the access physical
   links that can support ODU, or transparent client layers, both), as
   shown in {{fig-mpi1-otn-topo}} below.

~~~~
                   ...................................
                   :                                 :
                   :       +-----------------+       :
                   :       |                 |       :
           (R1)- - --------|                 |-------- - -(S31)
                   : AN1-1 |                 | AN1-7 :
                   :       |                 |       :
           (R3)- - --------|                 |       :
                   : AN1-2 |       AN1       |       :
                   :       |                 |       :
           (R4)- - --------|                 |-------- - -(S32)
                   : AN1-3 |                 | AN1-6 :
                   :       |                 |       :
                   :       +-----------------+       :
                   :          |          |           :
                   :    AN1-4 |          | AN1-5     :
                   :..........|..........|...........:

                              |          |
                            (S11)      (S12)
~~~~
{: #fig-mpi1-otn-topo title="OTN Abstract Topology exposed at MPI1 (MPI1 OTN Topology)"}

   The second TE Topology instance reports the domain 1 Ethernet
   abstract topology view (MPI1 ETH Topology), using the Ethernet
   technology-specific augmentations {{CLIENT-TOPO}}, with only one
   abstract TE node (i.e., AN1) and only access abstract TE links
   (which represent the access physical links which can support
   Ethernet client layers), as shown in {{fig-mpi1-eth-topo}} below.

~~~~
                   ...................................
                   :                                 :
                   :       +-----------------+       :
                   :       |                 |       :
           (R1)- - --------|                 |       :
                   : AN1-1 |                 |       :
                   :       |                 |       :
           (R2)- - --------|                 |       :
                   : AN1-8 |       AN1       |       :
                   :       |                 |       :
                   :       |                 |       :
                   :       |                 |       :
                   :       |                 |       :
                   :       +-----------------+       :
                   :                                 :
                   :.................................:
~~~~
{: #fig-mpi1-eth-topo title="ETH Abstract Topology exposed at MPI1 (MPI1 ETH Topology)"}

   The OTU4 trails on the inter-domain physical links (e.g., the link
   between S2 and S31) are pre-provisioned and exposed as external TE
   Links, within the MPI1 OTN topology (e.g., the external TE Link
   terminating on AN1-7 TE Link Termination Point (LTP) abstracting the
   OTU4 trail between S2 and S31).

   The PNC1 exports at MPI1 the following external TE Links, within the
   MPI1 OTN topology, representing the multi-function access links
   under its control:

   -  two abstract TE Links, terminating on LTP AN1-1 and AN1-2
      respectively, abstracting the physical access link between S3 and
      R1 and the access link between S6 and R3 respectively, reporting
      that they can support STM-64 client signals as well as ODU2
      connections;

   -  one abstract TE Link, terminating on LTP AN1-3, abstracting the
      physical access link between S6 and R4, reporting that it can
      support STM-64 client signals but no ODU2 connections.

   The information about the 10GE access link between S6 and R2 as well
   as the fact that the access link between S3 and R1 can also be
   configured as a 10GE link cannot be exposed by PNC1 within the MPI1
   OTN topology.

   Therefore, PNC1 exports at MPI1, within the MPI1 ETH topology, two
   abstract TE Links, terminating on LTP AN1-1 and AN1-8 respectively,
   abstracting the physical access link between S3 and R1 and the
   access link between S6 and R2 respectively, reporting that they can
   support Ethernet client signal with port-based and VLAN-based
   classifications.

   PNC1 should expose at MPI1 also the ODU termination and adaptation
   resources that are available to carry client signals (e.g.,
   Ethernet or STM-N) over OTN. This information is reported by the
   Tunnel Termination Points (TTPs) within the MPI1 OTN Topology.

   In particular, PNC1 will report, within the MPI1 OTN Topology, one
   TTP for each access link (i.e., AN1-1, AN1-2, AN1-3 and AN1-8) and
   will assign a transition link or an inter-layer lock identifier,
   which is unique across all the TE Topologies PNC1 is exposing at
   MPI1, to each TTP and access link's LTP pair.

   For simplicity purposes, this document assigns the same number to
   the LTP-ID, TTP-ID and ILL-ID that corresponds to the same access
   link (i.e., 1, 2, 3 and 8 respectively for the LTP, TTP and
   Inter-Layer Lock (IIL) corresponding with the access links AN1-1,
   AN1-2, AN1-3 and AN1-8).

   The PNC1 native topology would represent the physical network
   topology of the domain controlled by the PNC, as shown in
   {{fig-pnc1-topology}}.

~~~~
                  ..................................
                  :                                :
                  :     Physical Topology @ PNC1   :
                  :                                :
                  :        +----+        +----+    :
                  :        |    |S1-1    |    |S2-3:
                  :        | S1 |--------| S2 |----- - -(S31)
                  :        +----+    S2-1+----+    :
                  :     S1-2/               |S2-2  :
                  :    S3-4/                |      :
                  :    +----+   +----+      |      :
                  :    |    |3 1|    |      |      :
          (R1)- - -----| S3 |---| S4 |      |      :
                  :S3-1+----+   +----+      |      :
                  :   S3-2 \        \S4-2   |      :
                  :         \S5-1    \      |      :
                  :        +----+     \     |      :
                  :        |    |      \S8-2|      :
                  :        | S5 |       \   |      :
                  :        +----+        \  |S8-1  :
          (R2)- - ------  2/    \3        \ |      :
                  :S6-1 \ /5     \1        \|      :
                  :    +----+   +----+   +----+    :
                  :    |    |   |    |   |    |S8-5:
          (R3)- - -----| S6 |---| S7 |---| S8 |----- - -(S32)
                  :S6-2+----+4 2+----+4 3+----+    :
                  :     /         |        |       :
          (R3)- - ------     S7-3 |        | S8-4  :
                  :S6-3           |        |       :
                  :...............|........|.......:

                                  |        |
                                (S11)    (S12)
~~~~
{: #fig-pnc1-topology title="Physical Topology controlled by PNC1"}

   The PNC1 native topology is not exposed, and therefore it is the PNC's
   responsibility to abstract the whole domain physical topology as a
   single TE node and to maintain a mapping between the LTPs exposed at
   MPI abstract topologies and the associated physical interfaces
   controlled by the PNC:

~~~~
   Physical Interface     OTN Topology LTP     ETH Topology LTP
       (Figure 5)          (Figure 3)            (Figure 4)
           S2-3               AN1-7
           S3-1               AN1-1                 AN1-1
           S6-1                                     AN1-8
           S6-2               AN1-2
           S6-3               AN1-3
           S7-3               AN1-4
           S8-4               AN1-5
           S8-5               AN1-6
~~~~

   {{json-mpi1-otn-topo}}
   provides the detailed JSON code example ("mpi1-otn-
   topology.json") describing how the MPI1 ODU Topology is reported by
   the PNC1, using the {{!RFC8345}}, {{!RFC8795}} and {{OTN-TOPO}} YANG models,
   at MPI1.

   {{json-mpi1-eth-topo}}
   provides the detailed JSON code example ("mpi1-eth-
   topology.json") describing how the MPI1 ETH Topology is reported by
   the PNC1, using the {{!RFC8345}}, {{!RFC8795}} and {{CLIENT-TOPO}} YANG
   models, at MPI1.

   It is worth noting that this JSON code example does not provide all
   the attributes defined in the relevant YANG models, including:

   -  YANG attributes that are outside the scope of this document are
      not shown;

   -  The attributes describing the set of label values that are
      available at the inter-domain links (label-restriction container)
      are also not shown to simplify the JSON code example;

   -  The comments describing the rationale for not including some
      attributes in this JSON code example even if in the scope of this
      document are identified with the prefix "// comment" and
      included only in the first object instance (e.g., in the Access
      Link from the AN1-1 description or in the AN1-1 LTP description).

{: #domain2-topo}

### Domain 2 Black Topology Abstraction

   PNC2 provides the required black topology abstraction, as described
   in {{topology-description}}, to expose to the MDSC, at MPI2, two TE Topology
   instances with only one TE node each:

   -  the first instance reports the domain 2 OTN abstract topology
      view (MPI2 OTN Topology), with only one abstract node (i.e., AN2)
      and only inter-domain and access abstract TE links (which
      represent the inter-domain physical links and the access physical
      links that can support ODU, transparent client layers, or
      both);

   -  the instance reports the domain 2 Ethernet abstract topology view
      (MPI2 ETH Topology), with only one abstract TE node (i.e., AN2)
      and only access abstract TE links (which represent the access
      physical links which can support Ethernet client layers).

   PNC2 also reports the ODU termination and adaptation resources which
   are available to carry client signals (e.g., Ethernet or STM-N) over
   OTN in the TTPs within the MPI2 OTN Topology.

   In particular, PNC2 reports in both the MPI2 OTN Topology and MPI2
   ETH Topology an access link that abstracts the multi-function
   physical access link between S18 and R8, and terminates on the
   AN2-1 LTP that corresponds to the S18-3 physical interface,
   within the PNC2 native topology.  It also reports in the MPI2 ODU 
   Topology an AN2-1 TTP which abstracts the ODU termination and
   adaptation resources dedicated to this physical access link and
   the inter-layer lock between the AN2-1 TTP, and the AN2-1
   LTPs reported within the MPI2 OTN Topology and the MPI2 ETH Topology.

{: #domain3-topo}

### Domain 3 White Topology Abstraction

   PNC3 provides the required white topology abstraction, as described
   in {{topology-description}}, to expose to the MDSC, at MPI3, two TE Topology
   instances with multiple TE nodes, one for each physical node:

   -  the first instance reports the domain 3 OTN topology view (MPI3
      OTN Topology), with four TE nodes, which represent the four
      physical nodes (i.e. S31, S32, S33 and S34), and abstract TE
      links, which represent the inter-domain and internal physical
      links;

   -  the second instance reports the domain 3 Ethernet abstract
      topology view (MPI3 ETH Topology), with only two TE nodes, which
      represent the two edge physical nodes (i.e., S31 and S33) and
      only the two access TE links which represent the access physical
      links.

   PNC3 also reports the ODU termination and adaptation resources which
   are available to carry client signals (e.g., Ethernet or STM-N) over
   OTN in the TTPs within the MPI3 OTN Topology.

{: #multi-domain-topo}

### Multi-domain Topology Merging

   MDSC does not have any knowledge of the topologies of each domain
   until each PNC reports its abstract topologies, so the MDSC
   needs to merge these abstract topologies, provided by different
   PNCs, to build its topology view of the multi-domain network
   (MDSC multi-domain native topology), as described in section 4.3 of
   {{!RFC8795}}.

   The topology of each domain may be in an abstracted shape (refer to
   section 5.2 of {{!RFC8453}} for a different level of abstraction),
   while the inter-domain link information must be complete and fully
   configured by the MDSC.

   The inter-domain link information is reported to the MDSC by the two
   PNCs, controlling the two ends of the inter-domain link.

   The MDSC needs to know how to merge these inter-domain links. One
   possibility is to use the plug-id information, defined in {{!RFC8795}}:
   two inter-domain TE links, within two different MPI abstract
   topologies, terminating on two LTPs reporting the same plug-id value
   can be merged as a single intra-domain link, within any MDSC native
   topology.

   The value of the reported plug-id information can be either assigned
   by a central network authority and configured within the two PNC
   domains. Alternatively, it may be discovered using an automatic
   discovery mechanisms (e.g., LMP-based, as defined in {{?RFC6898}}).

   In the case a central authority assigns the plug-id values, it
   is under the central authority's responsibility to assign unique
   values.

   In case the plug-id values are automatically discovered, the
   information discovered by the automatic discovery mechanisms needs
   to be encoded as a bit string within the plug-id value. This
   encoding is implementation-specific, but the encoding rules need to
   be consistent across all the PNCs.

   In case of co-existence within the same network of multiple sources
   for the plug-id (e.g., central authority and automatic discovery or
   even different automatic discovery mechanisms), it is needed that
   the plug-id namespace is partitioned to avoid that different sources
   assign the same plug-id value to different inter-domain links. Also,
   the encoding of the plug-id namespace within the plug-id value is
   implementation-specific and will need to be consistent across all
   the PNCs.

   This document assumes that the plug-id is assigned by a central
   authority, with the first octet set to 0x00 to represent the central
   authority namespace. The configuration method used, within each PNC
   domain, are outside the scope of this document.

   For example, this document assumes that the following plug-id values
   are assigned, by administrative configuration, to the inter-domain
   links shown in {{fig-reference-network}}:

~~~~
        Inter-Domain Link     Plug-ID Value

           S2-S31               0x000231
           S7-S11               0x000711
           S8-S12               0x000812
           S8-S32               0x000832
           S12-S32              0x001232
           S15-S34              0x001534
~~~~

   Based on the plug-id values, the MDSC can merge the abstract
   topologies exposed by the underlying PNCs, as described in
   {{domain1-topo}}, {{domain2-topo}} and {{domain3-topo}} above, into its multi-domain native TE
   topology, as shown in {{fig-mdsc-topo}}.

~~~~
                ........................
                :                      :
                :   Network domain 1   :   .............
                :   Black Topology     :   :           :
                :     Abstraction      :   :  Network  :
                : AN1-1                :   :  domain 3 :
        (R1)- - ----------+            :   :  (White)  :
                :          \   +--------------+        :
        (R2)- - ---------+ +  /        :   :   \       :
                :         \| /         :   :    \      :
        (R3)- - --------- AN1 --+      :   :    S31 ---- - (R5)
                :         /|\    \     :   :   /   \   :   :
        (R4)- - ---------+ | \    +--------- S32   S33 - - (R6)
                :          |  \        :   :/  \   /   :
                :          |   +---+   :   /    S34    :
                :..........|.......|...:  /:   /       :
                           |       |     / :../........:
                           |       |    /    /
                ...........|.......|.../..../....
                :          |       |  /    /    :
                : Network  |       + /    /     :
                : domain 2 |      / /    /      :
                :          |     / /    /       :
                :          |    + / +--+        :
                :          |    |/ /            :
                : Black    +--- AN2 ------------- - -(R7)
                : Topology      | |     AN2-1   :
                : Abstraction   | +-------------- - -(R8)
                :               |               :
                :               +---------------- - -(R9)
                :                               :
                :...............................:
~~~~
{: #fig-mdsc-topo title="Multi-domain Abstract Topology controlled by an MDSC"}

{: #service-analysis}

## YANG Models for Service Configuration

   This section analyses how the MDSC can request the different PNCs to
   setup different multi-domains services, as described in {{service-description}},
   using the TE Tunnel YANG model, defined in {{TE-TUNNEL}}, with the OTN
   technology-specific augmentations, defined in {{OTN-TUNNEL}} with the
   client service YANG model defined in {{CLIENT-SIGNAL}}.

   The service configuration procedure is assumed to be initiated (step
   1 in {{fig-svc-setup}}) at the CMI from CNC to MDSC. Analysis of the CMI
   models (e.g., L1CSM, L2SM, VN) are outside the scope of this
   document, but it is assumed that the CMI YANG models provide all the
   information that allows the MDSC to understand that it needs to
   coordinate the setup of a multi-domain ODU data plane connection
   (which can be either an end-to-end connection or a segment
   connection) and, when needed, also the configuration of the
   adaptation functions in the edge nodes belonging to different
   domains.

~~~~
                                 |
                                 | {1}
                                 V
                          ----------------
                         |           {2}  |
                         | {3}  MDSC      |
                         |                |
                          ----------------
                           ^     ^      ^
                    {3.1}  |     |      |
                 +---------+     |{3.2} |
                 |               |      +----------+
                 |               V                 |
                 |           ----------            |{3.3}
                 |          |   PNC2   |           |
                 |           ----------            |
                 |               ^                 |
                 V               | {4.2}           |
             ----------          V                 |
            |   PNC1   |       -----               V
             ----------      (Network)        ----------
                 ^          ( Domain 2)      |   PNC3   |
                 | {4.1}   (          _)      ----------
                 V          (        )            ^
               -----       C==========D           | {4.3}
             (Network)    /  (       ) \          V
            ( Domain 1)  /     -----    \       -----
           (           )/                \    (Network)
           A===========B                  \  ( Domain 3)
          / (         )                    \(           )
      AP-1   (       )                      X===========Z
               -----                         (         ) \
                                              (       )   AP-2
                                                -----
~~~~
{: #fig-svc-setup title="Multi-domain Service Setup"}

   As an example, the objective in this section is to configure a
   connectivity service between R1 and R8, such as one of the services
   described in {{service-description}}.
   The inter-domain path is assumed to be R1
   \<-> S3 \<-> S1 \<-> S2 \<-> S31 \<-> S33 \<-> S34 \<->S15 \<-> S18 \<-> R8
   (see the physical topology in {{fig-reference-network}}).

   According to the different client signal types, different
   adaptations can be required to be configured at the edge nodes
   (i.e., S3 and S18).

   After receiving such request, MDSC determines the domain sequence,
   i.e., domain 1 \<-> domain 3 \<-> domain 2, with corresponding PNCs
   and the inter-domain links (step 2 in {{fig-svc-setup}}).

   As described in {{PATH-COMPUTE}}, the domain sequence can be
   determined by running the MDSC own path computation on the MDSC
   native topology, defined in {{multi-domain-topo}}, if and only if the MDSC
   has enough topology information. Otherwise, the MDSC can send path
   computation requests to the different PNCs (steps 2.1, 2.2 and 2.3
   in {{fig-svc-setup}}) and use this information to determine the optimal path
   on its internal topology and, therefore, the domain sequence.

   The MDSC will then decompose the tunnel request into a few TE tunnel
   segments and request different PNCs to setup each intra-domain TE
   tunnel segment (steps 3, 3.1, 3.2 and 3.3 in {{fig-svc-setup}}).

   The MDSC will take care of the configuration of both the intra-
   domain TE tunnel segments and inter-domain TE tunnel hand-off via
   corresponding MPI (using the TE tunnel YANG model defined in
   {{TE-TUNNEL}} and the OTN tunnel YANG model augmentations defined in
   {{OTN-TUNNEL}}) through all the PNCs controlling the domains selected
   during path computation. More specifically, for the inter-domain TE
   tunnel hand-off, taking into account that the inter-domain links are
   all OTN links, the list of timeslots and the TPN value assigned to
   that ODUk connection at the inter-domain link needs to be configured
   by the MDSC.

   The configuration of the timeslots and the TPN value used by the
   ODU2 connection on the internal links within a PNC domain (i.e., on
   the internal links within domain1) is outside the scope of this
   document, since it is a matter of the PNC domain internal
   implementation.

   However, the configuration of the timeslots used by the ODU2
   connection at the transport network domain boundaries (e.g., on the
   inter-domain links) needs to take into account the timeslots
   available on physical nodes belonging to different PNC domains
   (e.g., on node S2 within PNC1 domain and node S31 within PNC3
   domain). Each PNC provides to the MDSC, at the MPI, the list of
   available timeslots on the inter-domain links using the TE Topology

   YANG model and OTN Topology augmentation. The TE Topology YANG model
   in {{!RFC8795}} is being updated to report the label set information.
   See {{OTN-TOPO}} for more details.

   The MDSC, when coordinating the setup of a multi-domain ODU
   connection, also configures the data plane resources (i.e., the list
   of timeslots and the TPN) to be used on the inter-domain links. The
   MDSC can know the timeslots which are available on the physical OTN
   nodes terminating the inter-domain links (e.g., S2 and S31) from the
   OTN Topology information exposed, at the MPIs, by the PNCs
   controlling the OTN physical nodes (e.g., PNC1 and PNC3 controlling
   the physical nodes S2 and S31, respectively).

   In any case, the access link configuration is done only on the PNCs
   that control the access links (e.g., PNC-1 and PNC-3) and not on the
   PNCs of transit domain(s) (e.g., PNC-2). An access link will be
   configured by MDSC after the OTN tunnel is set up.

   Access configuration will vary and will be dependent on each type of
   service. Further discussion and examples are provided in the
   following sub-sections.

{: #odu-analysis}

### ODU Transit Service

   In this scenario, described in {{odu-description}}, the physical access
   links are configured as 10G OTN links and, as described in 
   {{topology-analysis}}, reported by each PNC as TE Links within the OTN abstract
   topologies they expose to the MDSC.

   When an IP link, between R1 and R8 is needed, the CNC requests, at
   the CMI, the MDSC to setup an ODU transit service.

   From its native topology, shown in {{fig-mdsc-topo}}, the MDSC understands,
   by means which are outside the scope of this document, that R1 is
   attached to the access link terminating on AN1-1 LTP in the MPI1 OTN
   Abstract Topology ({{fig-mpi1-otn-topo}}), exposed by PNC1, and that R8 is
   attached to the access link terminating on AN2-1 LTP in the MPI2
   Abstract Topology, exposed by PNC2.

   MDSC then performs multi-domain path computation (step 2 in
   {{fig-svc-setup}}) and requests PNC1, PNC2 and PNC3, at MPI1, MPI2 and MPI3
   respectively, to setup ODU2 (Transit Segment) Tunnels within the OTN
   Abstract Topologies they expose (MPI1 OTN Abstract Topology, MPI2
   OTN Abstract Topology and MPI3 OTN Abstract Topology, respectively).

   The MDSC requests, at MPI1, PNC1 to setup an ODU2 (Transit Segment)
   Tunnel with one primary path between AN-1 and AN1-7 LTPs, within the
   MPI1 OTN Abstract Topology ({{fig-mpi1-otn-topo}}), using the TE Tunnel YANG
   model, defined in {{TE-TUNNEL}}, with the OTN technology-specific
   augmentations, defined in {{OTN-TUNNEL}}:

   -  Source and Destination TTPs are not specified (since it is a
      Transit Tunnel): i.e., the source, src-tp-id, destination and
      dst-tp-id attributes of the TE tunnel instance are empty

   -  Ingress and egress points are indicated in the route-object-
      include-exclude list of the explicit-route-objects of the primary
      path:

       - The first element references the access link terminating on
          AN1-1 LTP

       - The last two element reference respectively the inter-domain
          link terminating on AN1-7 LTP and the data plane resources
          (i.e., the list of timeslots and the TPN) used by the ODU2
          connection over that link.

   {{json-mpi1-odu2-svc}}
   provides the detailed JSON code ("mpi1-odu2-service-
   config.json") describing how the setup of this ODU2 (Transit
   Segment) Tunnel can be requested by the MDSC, using the {{TE-TUNNEL}}
   and {{OTN-TUNNEL}} YANG models at MPI1.

   PNC1 knows, as described in the mapping table in {{domain1-topo}}, that
   AN-1 and AN1-7 LTPs within the MPI1 OTN Abstract Topology it exposes
   at MPI1 correspond to the S3-1 and S2-3 LTPs, respectively, within
   its native topology. Therefore it performs path computation for an
   ODU2 connection between these LTPs within its native topology, and
   sets up the ODU2 cross-connections within the physical nodes S3, S1
   and S2.

   Since the R1-S3 access link is a multi-function access link, PNC1
   also configures the OTU2 trail before setting up the ODU2
   cross-connection in node S3.

   As part of the OUD2 cross-connection configuration in node S2, PNC1
   configures the data plane resources (i.e., the list of timeslots and
   the TPN), to be used by this ODU2 connection on the S2-S31 inter-
   domain link, as requested by the MDSC.

   Following similar requests from MDSC to setup ODU2 (Transit Segment)
   Tunnels within the OTN Abstract Topologies they expose, PNC2 then
   sets up ODU2 cross-connections on nodes S31 and S33 while PNC3 sets
   up ODU2 cross-connections on nodes S15 and S18. PNC2 also configures
   the OTU2 trail on the S18-R8 multi-function access link.

#### Single Domain Example

   To setup an ODU2 end-to-end connection, supporting an IP link,
   between R1 and R3, the CNC requests, at the CMI, the MDSC to setup
   an ODU transit service.

   Following the procedures described in {{odu-analysis}}, MDSC requests
   only PCN1 to setup the ODU2 (Transit Segment) Tunnel between the
   access links terminating on AN-1 and AN1-2 LTPs within the MPI1
   Abstract Topology and PNC1 sets up ODU2 cross-connections on nodes
   S3, S5 and S6. PNC1 also configures the OTU2 trails on the R1-S3 and
   R3-S6 multi-function access links.

{: #epl-analysis}

### EPL over ODU Service

   In this scenario, described in {{evpl-description}}, the access links are
   configured as 10GE Links and, as described in {{topology-analysis}}, reported
   by each PNC as TE Links within the ETH abstract topologies they
   expose to the MDSC.

   When this IP link, between R1 and R8, is needed, the CNC requests,
   at the CMI, the MDSC to setup an EPL service.

   From its native topology, shown in {{fig-mdsc-topo}}, the MDSC understands,
   by means which are outside the scope of this document, that R1 is
   attached to the access link terminating on AN1-1 LTP in the MPI1 ETH
   Abstract Topology, exposed by PNC1, and that R8 is attached to the
   access link terminating on AN2-1 LTP in the MPI2 ETH Abstract
   Topology, exposed by PNC2.

   As described in {{domain1-topo}} and {{domain2-topo}}:

   -  the AN1-1 LTP, within the MPI1 ETH Abstract Topology, and the
      AN1-1 TTP, within the MPI1 OTN Abstract Topology, have the same
      IIL identifier (within the scope of MPI1);

   -  the AN2-1 LTP, within the MPI2 ETH Abstract Topology, and the
      AN2-1 TTP, within the MPI2 OTN Abstract Topology, have the same
      IIL identifier (within the scope of MPI2).

   Therefore, the MDSC also understands that it needs to coordinate the
   setup of a multi-domain ODU2 Tunnel between AN1-1 and AN2-1 TTPs,
   abstracting the ODU termination and adaptation resources on S3-1
   and S18-3 physical interfaces, within the OTN Abstract Topologies
   exposed by PNC1 and PNC2, respectively.

   MDSC then performs multi-domain path computation (step 2 in
   {{fig-svc-setup}}) and then requests:

   -  PNC1, at MPI1, to setup an ODU2 (Head Segment) Tunnel within the
      MPI1 OTN Abstract Topology;

   -  PNC1, at MPI1, to steer the Ethernet client traffic from/to AN1-1
      LTP, within the MPI1 ETH Abstract Topology, thought that ODU2
      (Head Segment) Tunnel;

   -  PNC3, at MPI3, to setup an ODU2 (Transit Segment) Tunnel within
      the MPI3 OTN Abstract Topology;

   -  PNC2, at MPI2, to setup ODU2 (Tail Segment) Tunnel within the
      MPI2 OTN Abstract Topology;

   -  PNC2, at MPI2, to steer the Ethernet client traffic to/from AN2-1
      LTP, within the MPI2 ETH Abstract Topology, through that ODU2
      (Tail Segment) Tunnel.

   MDSC requests, at MPI1, PNC1 to setup an ODU2 (Head Segment) Tunnel
   with one primary path between the AN1-1 TTP and AN1-7 LTP, within
   the MPI1 OTN Abstract Topology ({{fig-mpi1-otn-topo}}), using the TE Tunnel YANG
   model, defined in {{TE-TUNNEL}}, with the OTN technology-specific
   augmentations, defined in {{OTN-TUNNEL}}:

   -  Only the Source TTP (i.e., AN1 TE-Node and AN1-1 TTP) is
      specified (since it is a Head Segment Tunnel): therefore the
      Destination TTP is not specified

   -  The egress point in indicated in the route-object-include-exclude
      list of the explicit-route-objects of the primary path:

       - The last two element reference respectively the inter-domain
          link terminating on AN1-7 LTP and the data plane resources
          (i.e., the list of timeslots and the TPN) used by the ODU2
          connection over that link.

   Since there is not enough information about which client traffic
   should be steered to the OTN Tunnel, the ODU2 (Head Segment)
   Tunnel is setup with the administrative auto state, as defined in
   {{TE-TUNNEL}}.

   {{json-mpi1-odu2-tnl}}
   provides the detailed JSON code ("mpi1-odu2-tunnel-
   config.json") describing how the setup of this ODU2 (Head Segment)
   Tunnel can be requested by the MDSC, using the {{TE-TUNNEL}} and
   {{OTN-TUNNEL}} YANG models at MPI1.

   MDSC requests, at MPI1, PNC1 to steer the Ethernet client traffic
   from/to AN1-2 LTP, within the MPI1 ETH Abstract Topology ({{fig-mpi1-eth-topo}}),
   thought the MPI1 ODU2 (Head Segment) Tunnel, using the Ethernet
   Client YANG model, defined in {{CLIENT-SIGNAL}}.

   {{json-mpi1-epl-svc}}
   provides the detailed
   JSON code ("mpi1-epl-service-config.json") describing how the setup
   of this EPL service using the ODU2 Tunnel can be requested by the
   MDSC, using the {{CLIENT-SIGNAL}} YANG model at MPI1.

   PNC1 knows, as described in the table in {{domain1-topo}}, that the
   AN1-1 TTP and the AN1-7 LTP, within the MPI1 OTN Abstract Topology
   it exposes at MPI1, correspond to S3-1 TTP and S2-3 LTP,
   respectively, within its native topology. Therefore it performs path
   computation, for an ODU2 connection between S3-1 TTP and S2-3 LTP
   within its native topology, and sets up the ODU2 cross-connections
   within the physical nodes S3, S1 and S2, as shown in {{evpl-description}}.

   As part of the OUD2 cross-connection configuration in node S2, PNC1
   configures the data plane resources (i.e., the list of timeslots and
   the TPN), to be used by this ODU2 connection on the S2-S31 inter-
   domain link, as requested by the MDSC.

   After the configuration of the ODU2 cross-connection in node S3,
   PNC1 also configures the \[ETH -> (ODU)] and \[(ODU2) -> ETH]
   adaptation functions, within node S3, as shown in {{evpl-description}}.

   Since the R1-S3 access link is a multi-function access link, PNC1
   also configures the 10GE link before this step.

   Following similar requests from MDSC to setup ODU2 (Segment) Tunnels
   within the OTN Abstract Topologies, they expose as well as the
   steering of the Ethernet client traffic, PNC3 then sets up ODU2
   cross-connections on nodes S31 and S33 while PNC2 sets up ODU2
   cross-connections on nodes S15 and S18 as well as the \[ETH ->
   (ODU2)] and \[(ODU2) -> ETH] adaptation functions in node S18, as
   shown in {{evpl-description}}. PNC2 also configures the 10GE link on the
   S18-R8 multi-function access link.

{: #epl-domain1-analysis}

#### Single Domain Example

   When this IP link, between R1 and R2, is needed, the CNC requests,
   at the CMI, the MDSC to setup an EPL service.

   Following the procedures described in {{epl-analysis}}, the MDSC
   requests PCN1 to:

   -  Setup an ODU2 (end-to-end) Tunnel between the AN1-1 and AN1-2
      TTPs, abstracting S3-1 and S6-1 TTPs, within the MPI1 OTN
      Abstract Topology exposed by PNC1 at MPI1;

   -  Steer the Ethernet client traffic between the AN1-1 and AN1-8
      LTPs, exposed by PNC1 within MPI1 ETH Abstract Topology, through
      that ODU2 (end-to-end) Tunnel.

   Then PNC1 sets up ODU2 cross-connections on nodes S3, S5 and S6 as
   well as the \[ETH -> (ODU)] and \[(ODU2) -> ETH] adaptation functions
   in nodes S3 and S6, as shown in {{evpl-description}}. PNC1 also configures
   the 10GE link on the R1-S3 multi-function access link (the R2-S6
   access link has been pre-provisioned as a 10GE link, as described in
   {{multi-function-access}}).

{: #client-analysis}

### Other OTN Client Services

   In this scenario, described in {{client-description}}, the access links are
   configured as STM-64 links and, as described in {{topology-analysis}},
   reported by each PNC as TE Links within the OTN Abstract Topologies
   they expose to the MDSC.

   The CNC requests, at the CMI, MDSC to setup an STM-64 Private Line
   service between R1 and R8.

   Following similar procedures as described in {{epl-analysis}}, the MDSC
   understands that:

   -  R1 is attached to the access link terminating on AN1-1 LTP in the
      MPI1 OTN Abstract Topology, exposed by PNC1, and that R8 is
      attached to the access link terminating on AN2-1 LTP in the MPI2
      OTN Abstract Topology, exposed by PNC2;

   -  it needs to coordinate the setup of a multi-domain ODU2 Tunnel
      between the AN1-1 and AN2-1 TTPs, abstracting the ODU termination
      and adaptation resources on S3-1 and S18-3 physical interfaces,
      within the OTN Abstract Topologies exposed by PNC1 and PNC2,
      respectively.

   The MDSC then performs multi-domain path computation (step 2 in
   {{fig-svc-setup}}) and then requests:

   -  PNC1, at MPI1, to setup an ODU2 (Head Segment) Tunnel within the
      MPI1 OTN Abstract Topology;

   -  PNC1, at MPI1, to steer the STM-64 transparent client traffic
      from/to AN1-1 LTP, within the MPI1 OTN Abstract Topology, thought
      that ODU2 (Head Segment) Tunnel;

   -  PNC3, at MPI3, to setup an ODU2 (Transit Segment) Tunnel within
      the MPI3 OTN Abstract Topology;

   -  PNC2, at MPI2, to setup ODU2 (Tail Segment) Tunnel within the
      MPI2 OTN Abstract Topology;

   -  PNC2, at MPI2, to steer the STM-64 transparent client traffic
      to/from AN2-1 LTP, within the MPI2 ETH Abstract Topology, through
      that ODU2 (Tail Segment) Tunnel.

   PNC1, PNC2 and PNC3 then sets up the ODU2 cross-connections within
   the physical nodes S3, S1, S2, S31, S33, S15 and S18 as well as the
   \[STM-64 -> (ODU)] and \[(ODU2) -> STM-64] adaptation functions in
   nodes S3 and S18, as shown in {{client-description}}. PNC1 and PNC2 also
   configure the STM-64 links on the R1-S3 and R8-S18 multi-function
   access links, respectively.

#### Single Domain Example

   When an IP link, between R1 and R3, is needed, the CNC requests,
   at the CMI, the MDSC to setup an STM-64 Private Line service.

   The MDSC and PNC1 follow similar procedures as described in
   {{epl-domain1-analysis}} to set up ODU2 cross-connections on nodes S3, S5 and S6 as
   well as the \[STM-64 -> (ODU)] and \[(ODU2) -> STM-64] adaptation
   functions in nodes S3 and S6, as shown in {{client-description}}. PNC1 also
   configures the STM-64 links on the R1-S3 and R3-S6 multi-function
   access links.

{: #evpl-analysis}

### EVPL over ODU Service

   In this scenario, described in {{evpl-description}}, the access links are
   configured as 10GE links, as described in {{epl-analysis}} above.

   The CNC requests, at the CMI, the MDSC to setup two EVPL services:
   one between R1 and R2, and another between R1 and R8.

   Following similar procedures as described in {{epl-analysis}} and
   {{epl-domain1-analysis}}, MDSC understands that:

   -  R1 and R2 are attached to the access links terminating
      respectively on AN1-1 and AN1-8 LTPs in the MPI1 ETH Abstract
      Topology, exposed by PNC1, and that R8 is attached to the access
      link terminating on AN2-1 LTP in the MPI2 ETH Abstract Topology,
      exposed by PNC2;

   -  To setup the first (single-domain) EVPL service, between R1 and
      R2, it needs to coordinate the setup of a single-domain ODU0
      Tunnel between the AN1-1 and AN1-8 TTPs, abstracting S3-1 and
      S6-1 TTPs, within the OTN Abstract Topology exposed by PNC1;

   -  To setup the second (multi-domain) EPVL service, between R1 and
      R8, it needs to coordinate the setup of a multi-domain ODU0 Tunnel
      between the AN1-1 and AN2-1 TTPs, abstracting the ODU termination
      and adaptation resources on S3-1 and S18-3 physical interfaces,
      within the OTN Abstract Topologies exposed by PNC1 and PNC2,
      respectively.

   To setup the first (single-domain) EVPL service between R1 and R2,
   the MDSC and PNC1 follow similar procedures as described in
   {{epl-domain1-analysis}} to set up ODU0 cross-connections on nodes S3, S5 and S6 as
   well as the \[VLAN -> (ODU0)] and \[(ODU0) -> VLAN] adaptation
   functions, in nodes S3 and S6, as shown in {{evpl-description}}. PNC1 also
   configures the 10GE link on the R1-S3 multi-function access link.

   As part of the \[VLAN -> (ODU0)] and \[(ODU0) -> VLAN] adaptation
   functions configurations in nodes S2 and S6, PNC1 configures also
   the classification rules required to associate only the Ethernet
   client traffic received with VLAN ID 10 on the R1-S3 and R2-S6
   access links with this EVPL service. The MDSC provides this
   information to PNC1 using the {{CLIENT-SIGNAL}} model.

   To setup the second (multi-domain) EVPL service between R1 and R8,
   the MDSC, PNC1, PNC2 and PNC3 follows similar procedures as
   described in {{epl-analysis}} to setup the ODU0 cross-connections
   within the physical nodes S3, S1, S2, S31, S33, S15 and S18 as well
   as the \[VLAN -> (ODU0)] and \[(ODU0) -> VLAN] adaptation functions in
   nodes S3 and S18, as shown in {{evpl-description}}. PNC2 also configures
   the 10GE link on the R8-S18 multi-function access link (the R1-S3
   10GE link has been already configured when the first EVPL service
   has been setup).

   As part of the \[VLAN -> (ODU0)] and \[(ODU0) -> VLAN] adaptation
   functions configurations in nodes S3 and S18, PNC1 and,
   respectively, PNC2 also configures the classification rules required
   to associated only the Ethernet client traffic received with VLAN ID
   20 on the R1-S3 and R8-S18 access links with this EVPL service. The
   MDSC provides this information to PNC1 and PNC2 using the
   {{CLIENT-SIGNAL}} model.

{: #protection-analysis}

## YANG Models for Protection Configuration

{: #linear-protection-analysis}

### Linear Protection (end-to-end)

   As described in {{linear-protection-description}},
   the MDSC can decide to protect a
   multi-domain connectivity service by setting up ODU linear
   protection switching between edge nodes controlled by different PNCs
   (e.g., nodes S3 and S8, controlled by PNC1 and PNC2 respectively, to
   protect services between R1 and R8).

   MDSC performs path computation, as described in {{service-analysis}}, to
   compute both the paths for working and protection transport
   entities: the computed paths can pass through these exact PNC domains
   or through different transit PNC domains.

   Considering the case, described in {{linear-protection-description}}, where the working
   and protection transport entities pass through the same domain, MDSC
   would perform the same steps described in {{service-analysis}} to setup the
   ODU Tunnel and to configure the steering of the client traffic
   between the access links and the ODU Tunnel. The only differences
   are in the configuration of the ODU Tunnels.

   MDSC requests at the MPI1, PNC1 to setup an ODU2 (Head Segment)
   Tunnel within the MPI1 OTN Abstract Topology ({{fig-mpi1-otn-topo}}), using the
   TE Tunnel YANG model, defined in {{TE-TUNNEL}}, with the OTN
   technology-specific augmentations, defined in {{OTN-TUNNEL}}, with one
   primary path and one secondary path with 1+1 protection switching
   enabled:

   - Only the Source TTP (i.e., AN1-1 TTP) is specified (since it is a
      Head Segment Tunnel), as described in {{epl-analysis}};

   -  The egress point for the working transport entity in indicated in
      the route-object-include-exclude list of the explicit-route-
      objects of the primary path, as described in {{epl-analysis}};

   -  The protection switching end-point in indicated in the route-
      object-include-exclude list of the explicit-route-objects of the
      secondary path:

       - The first element references the TE-Node of the Source TTP
          (i.e., AN1 TE-Node);

   -  The egress point for the protection transport entity in indicated
      in the route-object-include-exclude list of the explicit-route-
      objects of the secondary path:

       - The last two element reference respectively the inter-domain
          link terminating on AN1-6 LTP and the data plane resources
          (i.e., the list of timeslots and the TPN) used by the ODU2
          connection over that link.

   PNC1 knows, as described in the table in {{domain1-topo}}, that the
   AN1-1 TTP, AN1-7 LTP and the AN1-6 LTP, within the MPI1 OTN Abstract
   Topology it exposes at MPI1, correspond to S3-1 TTP, S2-3 LTP and
   the S8-5 LTP, respectively, within its native topology. It also
   understands, from the route-object-include-exclude list of the
   explicit-route-objects of the secondary path configuration (whose
   last two elements represent an inter-domain link), that node S3 is
   the end-point of the protection group while the other end-point is
   outside of its control domain.

   PNC1 can perform path computation within its native topology and
   setup the ODU connections in nodes S3, S1, S2, S4 and S8 as well as
   configure the protection group in node S3.

{: #segmented-protection-analysis}

### Segmented Protection

   Under specific policies, it is possible to deploy a segmented
   protection for multi-domain services. The configuration of the
   segmented protection can be divided into a few steps, considering
   the example in {{segmented-protection-description}},
   the following steps would be used.

   MDSC performs path computation, as described in {{service-analysis}}, to
   compute all the paths for working and protection transport entities,
   which pass through the same PNC domains and inter-domain links: the
   MDSC would perform the same steps described in {{service-analysis}} to setup
   the ODU Tunnel and to configure the steering of the client traffic
   between the access links and the ODU Tunnel. The only differences
   are in the configuration of the ODU Tunnels.

   MDSC requests at the MPI1, PNC1 to setup an ODU2 (Head Segment)
   Tunnel within the MPI1 OTN Abstract Topology ({{fig-mpi1-otn-topo}}), using the
   TE Tunnel YANG model, defined in {{TE-TUNNEL}}, with the OTN
   technology-specific augmentations, defined in {{OTN-TUNNEL}}, with one
   primary path and one secondary path with 1+1 protection switching
   enabled:

   -  Only the Source TTP (i.e., AN1-1 TTP) is specified (since it is a
      Head Segment Tunnel), as described in {{epl-analysis}};

   -  The egress point (i.e., AN1-7 LTP) is indicated in the route-
      object-include-exclude list of the explicit-route-objects of the
      primary path, as described in {{epl-analysis}};

   -  The protection switching end-points are indicated in the route-
      object-include-exclude list of the explicit-route-objects of the
      secondary path:

       - The first element references the TE-Node of the Source TTP
          (i.e., AN1 TE-Node);

       - The last element references the TE-Node of the egress point
          (i.e., AN1 TE-Node).

   As described in {{epl-analysis}}, PNC1 knows that the AN1-1 TTP and the
   AN1-7 LTP, within the MPI1 OTN Abstract Topology it exposes at MPI1,
   correspond to S3-1 TTP and the S2-3 LTP, respectively, within its
   native topology. It also understands, from the route-object-include-
   exclude list of the explicit-route-objects of the secondary path

   configuration (the entire last element represent an abstract node
   terminating the inter-domain link used for the primary path), that
   the protection group should be terminated in nodes S3 and S2.

   PNC1 will perform path computations using its native topology and
   setup the ODU connections in nodes S3, S1, S2, S4 and S8 as well as
   configure the protection group in nodes S3 and S2.

   Following similar requests from MDSC to setup ODU2 (Segment)
   Tunnels, with segment protection, within the OTN Abstract Topologies
   they expose. PNC3 then sets up ODU2 cross-connections on nodes S31,
   S32, S33 and S34 and segment protection between nodes S31 and D34.
   PNC2 sets up ODU2 cross-connections on nodes S15, S12, S17 and S18
   and segment protection between nodes S15 and S18.

   MDSC stitch the configuration above to form its internal view of the
   end-to-end tunnel with segmented protection.

   Given the configuration above, the protection capability has been
   deployed on the tunnels. The head-end node of each domain can do the
   switching once there is a failure on one of the tunnel segments. For
   example, in Network domain 1, when there is a failure on the S1-S2
   lin, the head-end nodes S2 and S3 will automatically do the
   switching to S3-S4-S8-S2. This switching will be reported to the
   corresponding PNC (PNC1 in this example) and then MDSC. Other PNCs
   (PNC2 and PNC3 in this example) will not be aware of the failure and
   switching, nor do the nodes in network domains 2 and 3.

{: #notification-analysis}

## Notifications

   Notification mechanisms are required for the scenarios analyzed in
   this draft, as described in {{notification-description}}.

   The notification mechanisms are protocol-dependent. It is assumed
   that the RESTCONF protocol, defined in {{?RFC8040}} is optional, 
   and may be used at the MPIs mentioned in this document.

   From the perspective of MPI, the MDSC is the client while the PNC is
   acting as the server of the notification. The essential event
   streams, subscription and processing rules after receiving
   the notification can be found in section 6 of {{?RFC8040}}.
   
   Additional alarm reporting functions and alarm report management may
   be found in {{ITU-T_X.733}} and {{ITU-T_X.734}}
   
   Further detailed analysis of notification management is outside 
   the scope of this document.

{: #path-computation-analysis}

## Path Computation with Constraints

   The path computation constraints that can be supported at the MPI
   using the IETF YANG models defined in {{TE-TUNNEL}} and
   {{PATH-COMPUTE}}.

   When there is a technology-specific network (e.g., OTN), the
   corresponding technology (e.g., OTN) model should also be used to
   specify the tunnel information on MPI, with the constraint included
   in TE Tunnel model.

   Further detailed analysis is outside the scope of this document.

# Security Considerations

   This document analyses the applicability of the YANG models being
   defined by the IETF to support OTN single and multi-domain
   scenarios.

   When deploying ACTN functional components, the securing of external
   interfaces and hardening of resource datastores, the protection of
   confidential information, and limit the access to function,
   should all be carefully considered.  Section 9 of {{!RFC8453}}
   highlights that implementations should consider encrypting data that
   flows between key components, especially when they are implemented
   at remote nodes. Further discussion on securing the interface between
   the MDSC and PNCs via the MDSC-PNC Interface (MPI) are discussed in
   section 9.2 of {{!RFC8453}}.

   The YANG modules highlighted in this document are designed to be
   accessed via network configuration protocols such as NETCONF
   {{?RFC6241}} or RESTCONF {{?RFC8040}}. When using NETCONF, utilizing a
   secure transport via Secure Shell (SSH) {{?RFC6242}} is mandatory. If
   using RESTCONF, then secure transport via TLS {{?RFC8446}} is
   mandatory. When using either NETCONF or RESTCONF, the use of Network
   Configuration Access Control Model (NACM) {{?RFC8341}} may be used to
   restrict access to specific protocol operations and content.

## OTN Security

   Inherently OTN networks ensure privacy and security via hard
   partitioning of traffic onto dedicated circuits. The separation of
   network traffic makes it difficult to intercept data transferred
   between nodes over OTN-channelized links.

   Within OTN environments, the (General Communication Channel) GCC is used for OAM
   functions such as performance monitoring, fault detection, and
   signaling. The GCC control channel should be secured using a
   suitable mechanism.

# IANA Considerations

   This document requires no IANA actions.

--- back

{: #json-validation}

# Validating a JSON fragment against a YANG Model

   The objective is to have a tool that allows validating whether a
   piece of JSON code embedded in an Internet-Draft is compliant with a
   YANG model without using a client/server.

## JSON CODE

   This document provides some detailed JSON code examples to describe
   how the YANG models being developed by the IETF (TEAS and CCAMP WG
   in particular) may be used. The scenario examples are provided using
   JSON to facilitate readability.

   Different objects need to have an identifier. The convention used to
   create mnemonic identifiers is to use the object name (e.g., S3 for
   node S3), followed by its type (e.g., NODE), separated by a "-",
   followed by "-ID". For example, the mnemonic identifier for AN1
   would be AN1-NODE-ID.

   The JSON language does not inherently support the insertion of comments. 
   This document will insert comments into the JSON code as JSON name/value
   pair with the JSON name string starting with the "//" characters.
   For example, when describing the example of a TE Topology instance
   representing the ODU Abstract Topology exposed by the Transport PNC,
   the following comment has been added to the JSON code:

~~~~
      "// comment": "ODU Abstract Topology @ MPI",
~~~~

   The JSON code examples provided in this document have been validated
   against the YANG models following the validation process described
   in {{json-validation}}, which would not consider the comments.

   To have successful validation of the examples, some numbering scheme
   has been defined to assign identifiers to the different entities
   which would pass the syntax checks. In that case, to simplify the
   reading, another JSON name/value pair formatted as a comment and
   using the mnemonic identifiers is also provided. For example, the
   identifier of AN1 (AN1-NODE-ID) has been assumed to be "192.0.2.1"
   and would be shown in the JSON code example using the two JSON
   name/value pair:

~~~~
      "// te-node-id": "AN1-NODE-ID",

      "te-node-id": "192.0.2.1",
~~~~

   The first JSON name/value pair will be automatically removed in the
   first step of the validation process, while the second JSON
   name/value pair will be validated against the YANG model
   definitions.

##  Manipulation of JSON fragments

   This section describes the various ways JSON fragments are used in
   the I-D processing and how to manage them.

   Let's call "folded-JSON" the JSON embedded in the I-D: it fits the
   72 chars width and it is acceptable for it to be invalid JSON.

   We then define "unfolded-JSON" a valid JSON fragment having the same
   contents of the "folded-JSON " without folding, i.e. limits on the
   text width. The folding/unfolding operation may be done according to
   {{?RFC8792}}. The "unfolded-JSON" can be edited by the authors using
   JSON editors with the advantages of syntax validation and pretty-
   printing.

   Both the "folded" and the "unfolded" JSON fragments can include
   comments having descriptive fields and directives we'll describe
   later to facilitate the reader and enable some automatic processing.

   The presence of comments in the "unfolded-JSON" fragment makes it an
   invalid JSON encoding of YANG data. Therefore we call "naked JSON"
   the JSON where the comments have been stripped out: not only it is
   valid JSON but it is a valid JSON encoding of YANG data.

   The following schema resumes these definitions:

~~~~
                       unfold_it -->             stripper -->

             Folded-JSON           Unfolded-JSON             Naked JSON

                       <-- fold_it              <-- author edits

   <=72-chars?    must              may                      may

   valid JSON?     may             must                     must

   JSON-encoding
   of YANG data?   may              may                     must
~~~~

   The validation toolchain has been designed to take a JSON in any of
   the three formats and validate it automatically against a set of
   relevant YANG modules using available open-source tools.
   
   The tool used to validate the JSON examples in this document can be
   found at: https://github.com/ietf-ccamp-wg/json-yang/tree/2.2

##  Comments in JSON fragments

   We found it useful to introduce two kinds of comments, both defined as
   key-value pairs where the key starts with "//":

   - free-form descriptive comments, e.g."// comment" : "refine this"
   to describe properties of JSON fragments.

   - machine-usable directives e.g. "// header" : {"reference-drafts" : {
   "ietf-routing-types@2017-12-04": "rfc8294",}} which can be used to
   automatically download from the network the relevant I-Ds or RFCs
   and extract from them the YANG models of interest. This is
   particularly useful to keep consistency when the drafting work is
   rapidly evolving.

##  Validation of JSON fragments: DSDL-based approach

   The idea is to generate a JSON driver file (JTOX) from YANG, then
   use it to translate JSON to XML and validate it against the DSDL
   schemas, as shown in {{fig-dsdl-approach}}.

   Useful link: https://github.com/mbj4668/pyang/wiki/XmlJson

~~~~
                           (2)
               YANG-module ---> DSDL-schemas (RNG,SCH,DSRL)
                      |                  |
                      | (1)              |
                      |                  |
      Config/state  JTOX-file            | (4)
             \        |                  |
              \       |                  |
               \      V                  V
      JSON-file------------> XML-file ----------------> Output
                 (3)
~~~~
{: #fig-dsdl-approach title="DSDL-based approach for JSON code validation"}

   In order to allow the use of comments following the convention
   defined in {{conventions}}, without impacting the validation process,
   these comments will be automatically removed from the JSON-file that
   will be validated.

##  Validation of JSON fragments: why not using an XSD-based approach

   This approach has been analyzed and discarded because no longer
   supported by pyang.

   The idea is to convert YANG to XSD, JSON to XML and validate it
   against the XSD, as shown in {{fig-xsd-approach}}:

~~~~
                     (1)
         YANG-module ---> XSD-schema - \       (3)
                                        +--> Validation
         JSON-file------> XML-file ----/
                     (2)
~~~~
{: #fig-xsd-approach title="XSD-based approach for JSON code validation"}

   The pyang support for the XSD output format was deprecated in 1.5
   and removed in 1.7.1. However, pyang 1.7.1 is necessary to work with
   YANG 1.1 so the process shown in {{fig-xsd-approach}}
   will stop just at step (1).

{: #json}

# Detailed JSON Examples

   The JSON code examples provided in this appendix have been validated
   using the tools in {{json-validation}} and folded using the tool in
   {{?RFC8792}}.

{: #json-topo}

## JSON Examples for Topology Abstractions

{: #json-mpi1-otn-topo}

### JSON Code: mpi1-otn-topology.json

This is the JSON code reporting the OTN Topology @ MPI1:

~~~~ ascii-art
{::include ./mpi1-otn-topology.txt}
~~~~
{: artwork-name="mpi1-otn-topology.txt"}

{: #json-mpi1-eth-topo}

### JSON Code: mpi1-eth-topology.json

This is the JSON code reporting the ETH Topology @ MPI1:

~~~~ ascii-art
{::include ./mpi1-eth-topology.txt}
~~~~
{: artwork-name="mpi1-eth-topology.txt"}

{: #json-svc}

## JSON Examples for Service Configuration

{: #json-mpi1-odu2-svc}

### JSON Code: mpi1-odu2-service-config.json

This is the JSON code reporting the ODU2 transit service configuration @ MPI1:

~~~~ ascii-art
{::include ./mpi1-odu2-service-config.txt}
~~~~
{: artwork-name="mpi1-odu2-service-config.txt"}

{: #json-mpi1-odu2-tnl}

### JSON Code: mpi1-odu2-tunnel-config.json

   This is the JSON code reporting the ODU2 head tunnel segment
   configuration @ MPI1:

~~~~ ascii-art
{::include ./mpi1-odu2-tunnel-config.txt}
~~~~
{: artwork-name="mpi1-odu2-tunnel-config.txt"}

{: #json-mpi1-epl-svc}

### JSON Code: mpi1-epl-service-config.json

This is the JSON code reporting the EPL service configuration @ MPI:

~~~~ ascii-art
{::include ./mpi1-epl-service-config.txt}
~~~~
{: artwork-name="mpi1-epl-service-config.txt"}

{: numbered="false"}

# Acknowledgments

   The authors would like to thank all members of the Transport NBI
   Design Team involved in the definition of use cases, gap analysis
   and guidelines for using the IETF YANG models at the Northbound
   Interface (NBI) of a Transport SDN Controller.

   The authors would like to thank Xian Zhang, Anurag Sharma, Sergio
   Belotti, Tara Cummings, Michael Scharf, Karthik Sethuraman, Oscar
   Gonzalez de Dios, and Hans Bjursrom for having initiated
   the work on gap analysis for transport NBI and having provided
   foundations work for the development of this document.

   The authors would like to thank the authors of the TE Topology and
   Tunnel YANG models {{!RFC8795}} and {{TE-TUNNEL}}, in particular, Igor
   Bryskin, Vishnu Pavan Beeram, Tarek Saad and Xufeng Liu, for their
   support in addressing any gap identified during the analysis work.

   The authors would like to thank Henry Yu and Aihua Guo for their
   input and review of the URIs structures used within the JSON code
   examples.

   This work was supported in part by the European Commission funded
   H2020-ICT-2016-2 METRO-HAUL project (G.A. 761727).

   This document was prepared using kramdown.

   Previous versions of this document was prepared using 2-Word-v2.0.template.dot.
