# Weekly Call (October 2nd, 2019)

## Attendees
- Italo Busi
- Daniel King
- Gianmarco Bruno
- Sergio Belotti
- Yuji Tochio

## Agenda:

1) Work plan for CCAMP WG LC
2) DT Review of the Applicability Statement I-D
3) DT Review of the JSON code examples
4) AOB

## Meeting Notes:

### 1) Work plan for CCAMP WG LC

Draft text under review in [pull request #66](https://github.com/danielkinguk/transport-nbi/pull/66)

Review of the latest version of JSON code examples started with [pull request #78](https://github.com/danielkinguk/transport-nbi/pull/78)

The tentative plan is:

- complete the review of the draft and of the JSON code examples by October 13, 2019
- address any unresolved comments in the DT on October 16, 2019
- submit an I-D ready for WG LC by October 21, 2019

### 2) DT Review of the Applicability Statement I-D

The latest version is available within [pull request #66 comment](https://github.com/danielkinguk/transport-nbi/pull/66#issuecomment-516900414)

Waitng for reviews from Daniel and Dieter:

- Daniel should provide his review comments by tomorrow (October 3, 2019) EOB

- **Action (Italo) - Check with Dieter his availability to provide the next round of comments**


Comments against the clean-up copy are preferred

Reviewed the status of the open issues pending resolution:

- [#46](https://github.com/danielkinguk/transport-nbi/issues/46): to be addressed by Daniel by tomorrow (October 3, 2019) EOB
- [#72](https://github.com/danielkinguk/transport-nbi/issues/72): closed during this call. Agreement to leave the JSON code examples in the appendix since it is quite a lot of code.
- [#75](https://github.com/danielkinguk/transport-nbi/issues/75): to be addressed by Daniel by tomorrow (October 3, 2019) EOB
- [#77](https://github.com/danielkinguk/transport-nbi/issues/77): mail sent, waiting from actions from TE tunnel model authors. This action is not blocking for WG LC

### 3) DT Review of the JSON code examples

Sergio and Haomian committed to review the updated JSON code examples before October 13, 2019

Any other member of the DT is welcome to review and submit comments to the pull request

Gianmarco will give us a short tutorial on how to use his tool to validate and fold JSON code examples so anybody within the DT can validate and fold the JSON code examples

Quick introduction and review of the updated JSON cod examples:

- ETH TE Topology
  - Label restrictions in the ETH TE Topology should be empty because the VLAN range available for VLAN classification is reported within the eth-svc container.

- ODU2 Service:
  - c/explicit-route-objects/explicit-route-objects-always/
  - c/num-unnum-hop/numbered-link-hop/

- ODU2 Tunnel
  - c/index=1/index=2/ in the second ERO element

Agreed to add also the ETH Topology JSON code example to the draft

**Action (Italo) - Update the JSON code examples**

### 4) AOB

Italo has been contacted offline about the possibility to send a LS to MEF about the DT work

This is related to [open issue #21](https://github.com/danielkinguk/transport-nbi/issues/21): Daniel will check offline about the process for engaging with MEF experts to them take into account the DT work

Next call is planned on October 16, 2019 at 3pm CEST

The objectives of the next call are:

- Gianmarco tutorial on the tool fo JSON code validation and folding

- Resolve review comments on the text and and on the JSON code that requires DT call discuss

# Note Takers

- Italo Busi
