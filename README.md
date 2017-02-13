# transport-nbi

From: CCAMP [mailto:ccamp-bounces@ietf.org] On Behalf Of Daniele Ceccarelli
Sent: 25 October 2016 13:50
To: CCAMP (ccamp@ietf.org) <ccamp@ietf.org>
Cc: ccamp-chairs@ietf.org
Subject: [CCAMP] Transport NBI - Design Team

Dear CCAMP,

We (chair and AD) decided to create a design team with the aim to work on the definition of technology specific extensions to the NBI of Transport controller.

Problem Statement:
Transport networks, such as Optical Transport Network (OTN) and Wavelength Division Multiplexing (WDM) networks, are built using equipment from a single vendor and are managed using proprietary interfaces to dedicated Element Management Systems (EMS) / Network Management Systems (NMS). A common open interface to each domain controller/management system is pre-requisite for network operators to control multi-vendor/multi-domain networks and enable also service provisioning coordination/automation.
This can be achieved by using standardized YANG models, used together with an appropriate protocol (e.g., RESTCONF). However, there is often confusion of how the existing models in IETF can be used for transport networks. Furthermore, there is no clear answer to the question of whether there is missing information for the control of specific technologies in the existing models (available in IETF or other SDOs) or even missing models since existing drafts focus on providing only the YANG models and explanation around them.
Draft-zhang-ccamp-transport-yang-gap-analysis-00 already provides an overview of the problem.

Goals/Deliverables:
- Use cases and Gap analysis: identify a set of technologies use cases and providing a gap analysis against existing models 
- Missing YANG models: Document  requirements for new models or, where possible, as augmentation of existing IETF models. Coordinate requirements with appropriate WGs, e.g., TEAS, RTGWG and CCAMP itself.
- Guidelines: Providing guidelines in terms of how all the related models can be used in a step-wise manner, using a couple of well identified transport network use cases.

Relationship with other work:
The control of transport networks in general is covered by mechanisms defined in the TEAS WG. That WG is expected to produce base models that may require technology specific augmentations.
The Transport NBI is applicable to the ACTN (Abstraction and Control of TE Networks) architecture defined in the TEAS WG, and the scope of the DT may be applicable to the technology specific extensions of the ACTN MPI interface (MDSC-PNC interface).

If you are willing to candidate yourself as a member of the Transport NBI DT please send an email to the CCAMP chairs and secretary within Friday November 4th.

Daniele & Fatai
