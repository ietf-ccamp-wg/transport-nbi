# Weekly Call (June 6, 2018)

## Attendees

- Italo Busi  
- Daniel King  
- Gianmarco Bruno  
- Yuji Tochio  
  

## Agenda:
  
1) Handling JSON long lines in Internet-Draft  
2) Topology Identifiers (I2RS and TEAS)  
3) AOB  
  

## Meeting Notes:

### 1) Handling JSON long lines in Internet-Draft

  
Reference: [draft-kwatsen-netmod-artwork-folding-00](https://tools.ietf.org/html/draft-kwatsen-netmod-artwork-folding-00)  
  
We think it will be useful for our work and would like to share our feedback.  
It would be great to have line breaking based on words and not chars to increase readibility for humans.  
The script produces text which is not valid JSON anymore: a command line shell is required to make the conversion.  
Finally it would be good for our DT to have rfcstip tool able to extract JSON examples other than YANG models.  
For the time being we will keep both valid JSON (not shortened) and shortened (txt).  

***Action: Gianmarco with Italo and Daniel (others welcome) will start a draft about comments and keywords in JSON***

### 2) Topology Identifiers (I2RS and TEAS)


Reference: [Pull Request #10](https://github.com/danielkinguk/transport-nbi/pull/10)  
  
Discussion postponed to next week DT call  

### 3) AOB

[Pull Request #29](https://github.com/danielkinguk/transport-nbi/pull/29) for ODU2 and EPL Service Examples is under review in GitHub.

A future update is expected as soon as the TE and OTN Tunnel models are updated.  
  
New OTN tunnel model will be available soon.  
  
Status update of some open issues in GitHub:  
- [Pull Request #28](https://github.com/danielkinguk/transport-nbi/issues/28)  
- [Pull Request #23](https://github.com/danielkinguk/transport-nbi/issues/23)  
- [Pull Request #21](https://github.com/danielkinguk/transport-nbi/issues/21)  
  
The next DT call is planned for next week June 13, 2018 at 3pm CEST  
  
# Note Takers

- Italo Busi  
- Gianmarco Bruno  
