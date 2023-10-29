# transport-nbi

Google Group List: https://groups.google.com/g/transport-nbi-dt

Active survey to establish next design team milestones: https://23jmszz1fks.typeform.com/to/qv6zuPTW

Design Team Members
- Aihua Guo
- Nigel Davis
- Dieter Beller
- Gianmarco Bruno
- Haomian Zheng
- Italo Busi
- Monali Chakrabarty
- Oscar Dios Gonzalez
- Scott Mansfield
- Sergio Belotti
- Luis Miguel Contreras Murillo
- Julien Meuric
- Prasenjit Manna
- Daniel King

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

## Output 

The first document from the Design Team was:

Transport Northbound Interface Applicability Statement
https://datatracker.ietf.org/doc/html/draft-ietf-ccamp-transport-nbi-app-statement-17

It is anticipated that future output from the design team will be in the form of Wiki documentation and GitHub code/examples. 

## Contributing

This repository relates to activities in the Internet Engineering Task Force
([IETF](https://www.ietf.org/)). All material in this repository is considered
Contributions to the IETF Standards Process, as defined in the intellectual
property policies of IETF currently designated as
[BCP 78](https://www.rfc-editor.org/info/bcp78),
[BCP 79](https://www.rfc-editor.org/info/bcp79) and the
[IETF Trust Legal Provisions (TLP) Relating to IETF Documents](http://trustee.ietf.org/trust-legal-provisions.html).

Any edit, commit, pull request, issue, comment or other change made to this
repository constitutes Contributions to the IETF Standards Process
(https://www.ietf.org/).

You agree to comply with all applicable IETF policies and procedures, including,
BCP 78, 79, the TLP, and the TLP rules regarding code components (e.g. being
subject to a Simplified BSD License) in Contributions.


### Other Resources

Discussion of this work occurs on the
[CCAMP working group mailing list](https://mailarchive.ietf.org/arch/browse/ccamp/)
([subscribe](https://www.ietf.org/mailman/listinfo/ccamp)).  In addition to
contributions in GitHub, you are encouraged to participate in discussions there.

**Note**: Some working groups adopt a policy whereby substantive discussion of
technical issues needs to occur on the mailing list.

You might also like to familiarize yourself with other
[working group documents](https://datatracker.ietf.org/wg/ccamp/documents/).
