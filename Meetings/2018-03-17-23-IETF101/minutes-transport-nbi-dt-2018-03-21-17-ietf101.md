# Transport NBI DT @ IETF 101 - March 21, 2018

## Attendees

- Italo Busi
- Yunbin Xu
- Dieter Beller
- Sergio Belotti
- Haomian Zheng
- Qilei Wang
- Xiaobing Niu
- Yuji Tochio

## Agenda:

1) Relationship with TE Tutorial
2) OpenConfig
3) Inter-domain link and tunnel stitching
4) Multi-layer architecture issue

## Meeting Notes:

### 1) Relationship with TE Tutorial

Reviewed the output of the discussion with Igor:

https://github.com/danielkinguk/transport-nbi/issues/19

The proposed approach seems reasonable.

**Action (Italo): Send a summary mail to the CCAMP and TEAS WG mailing lists.**

**Action: Review in details the two drafts to understand which text should be moved into the TE Tutorial and which text should be replaced with a reference to the TE Tutorial.**

### 2) OpenConfig

The OC model is structured with a set of different Yang models folders. One of them is specific for optical transport, composed by:
-terminal device model
-optical amplifier model
-transport-line-common model
-transport-line-protection model
-channel-monitor model
-wavelength-router model

See https://github.com/openconfig/public/tree/master/release/models/optical-transport  for more details.

The model is dealing with L0 only for the moment for optical part (not L1).

The model is defining a “logical channel” entity for any part of the network from client to line , so form client to line of an optical transport node, there is a “pipe” of logical channel.

The ethernet model has also been reviewed.

At the first glance it appears no attributes/structures can be easily reused for the scope of the DT.

**Action: Review in details the OpenConfig model to check if there is something which can be used by the TNBI DT or confirm that there is nothing that can be reused.**

For the OTN client services, the current working assumption is that DT analyses the YANG models in:

https://tools.ietf.org/html/draft-zheng-ccamp-otn-client-signal-yang

### 3) Inter-domain link and tunnel stitching

We have clarified that the current working assumptions are that:

a) the MDSC discover the inter-domain links using the plug-id values that are administratively configured

b) MDSC decides which label should be used by a tunnel on inter domain links and configured them when setting up the tunnel segments in the two adjacent domains

When setting up a tunnel segment at the MPI, the MDSC configures the ingress/egress inter-domain link and the label corrisponding label in the first/last elements of the route-object-include-exclude list.

The TNBI Applicability statement I-D will be updated to make sure its content is consistent with these assumptions.

### 4) Multi-layer architecture issue

Theoretically the issue applies not only to the IP over Optical scenario but in general to any multi-layer scenario e.g. in case of ODU over OCh/OTSiA, when the ODU network and the WDM network belong to the same provide but are managed by different departments.

**Action: Validate whether it is possible that ODU and WDM networks are managed by different departments.**
