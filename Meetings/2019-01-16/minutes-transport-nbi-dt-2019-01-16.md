# Weekly Call (January 16, 2019) 

## Attendees  
- Daniel King  
- Gianmarco Bruno  
- Italo Busi  
- Sergio Belotti  

## Agenda:  

1) Follow-up tooling discussions  
2) Applicability Statement I-D update review  
3) Planning for next steps  
4) AOB  

## Meeting Notes:  
  
### 1) Follow-up tooling discussions  

[Open Issue # 54](https://github.com/danielkinguk/transport-nbi/issues/54): Review of the existing tools presented in the RTGWG meeting at IETF 103

With pyang moving from 1.7.1 to 1.7.5, the DSDL checking is no longer supported. Instead libyang is more updated than pyang, besides being much faster  
We willl use libyang to compile the JSON instance, then pyang is preferable to validate the YANG model itself  

Two issues have been found with pyang validation:  
*   it does not detect the mistake when a namespace which should not be present is used
*   it does not manage YANG features

**Actions:**  
- Check that libyang does not have the issues identified with pyang validation (Gianmarco)  
- Need to update the validation toolchain to use libyang instead of pyang (Gianmarco)  
- Need to update appendix when libyang being used (Gianmarco)  
- Email Benoit and let ask him if there is a preference, also how are IETF I-D JSON examples typically vallidated (Italo)  

[Open Issue #39](https://github.com/danielkinguk/transport-nbi/issues/39): move appendix A of the Applicability Statement I-D into another Netmod I-D  

**Actions:**  
- We can move Appendix A into a new informational I-D and propose to NETMOD: check also with Benoit (Italo)  

### 2) Applicability Statement I-D update review  

[Latest version](https://github.com/danielkinguk/transport-nbi/commit/824fd94bc98ab12949ad5a451eda262865294cdb) uploaded on January 7, 2019

**Actions:**  
- All, please review when italo posts the update version (ETA Jan 18).   
- Both Sergio and Dan will review, ideally providing comments back to Italo before Jan 30, or Feb 6 at latest.   
- Planning to submit next version of I-D before IETF 104  

### 3) Planning for next steps  

Agreed to postpone to IETF 105:  
- pull request [#38](https://github.com/danielkinguk/transport-nbi/pull/38)  
- open issues: [#31](https://github.com/danielkinguk/transport-nbi/issues/31); [#39](https://github.com/danielkinguk/transport-nbi/issues/39); [#45](https://github.com/danielkinguk/transport-nbi/issues/45); [#50](https://github.com/danielkinguk/transport-nbi/issues/50) and [#51](https://github.com/danielkinguk/transport-nbi/issues/51)

Daniel will take responsability for [Open Issue #21](https://github.com/danielkinguk/transport-nbi/issues/21) after the next update planned in February  

We will review the plan for the other open issues (with no milestones) after IETF 104  

### 4) AOB  

Next call is planned for January 30, 2019 at 3pm CET  

## Note Takers  
- Italo Busi  
- Daniel King  
- Gianmarco Bruno
