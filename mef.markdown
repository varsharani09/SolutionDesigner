---
layout: page
title: MEF
permalink: /mef/
---

**SPIKE: ICA RTT PAF Operationalization & Integration**
 
| ------------- |:-------------:| 
| Document Number:1      | [Reference JIRA link](https://jira3.cerner.com/browse/CTSMONETFB-2955)| 
| Revision: V1.0     | Title:SPIKE: ICA RTT PAF Operationalization & Integration      |   
| Author:Varsharani Dhupadale | Signature / Date:Approved/1st  April, 2020      | 
| Approver 1:Avazpour Jim | Signature / Date: |
| Approver 2:Kumar R P Pavan | Signature / Date: |
| Approver 3:Kumar R P Pavan | Signature / Date: |


**Table of Contents-**

1.	INTRODUCTION
    
2.	PURPOSE

3.	MODULES INVOLVED
    
4.	DEFINITIONS

5.	REFERENCES

6.	DETAILED REQUIREMENTS

7.	REQUIRED DETAILS

8.	FORM / REPORT SPECIFICATIONS

9.	TESTING CONSIDERATIONS

10.	APPENDICES / ATTACHMENTS

 
**1.  Introduction-**

ICA Round Trip Time (RTT) is a measure of network latency. Specifically, ICA RTT is the time it takes for data to travel from the user device to a Citrix server and back to the user device. The higher this measure, the slower the system will seem to the end-user. Currently, ICA RTT data is tracked for individual Cerner users by the minute. Measurements of less than 300 ms are considered “normal” for Cerner clients, while anything higher is deemed abnormal and could have a negative impact on the user experience. 

When a certain number of users at a client site begin to experience ICA RTT higher than 300ms, this will be recorded as an ICA RTT PAF (Performance Abnormality Flag). ICA RTT PAFs are assigned a “Dispersion Score” ranging from 0-100 based on the number of end-users impacted per client site. Dispersion scores of less than 30 indicate the issue is confined to a specific subnet and is not impacting a high volume of users. Dispersion scores greater than 50 indicate a broad impact and point to an issue within the Cerner network as the root cause of the high ICA RTT. SSE monitoring teams will therefore focus on widely dispersed ICA RTT PAFs. 

**2.	Purpose-**
The purpose of this story is to identify the sources of ICA RTT PAF data and to investigate how this data can be integrated with the NOC monitoring tools to generate proactive alerts.

**3.	Modules Involved-**

NA

**4.	Definitions-**

| Short Forms        | Full Forms           |
| ------------- |:-------------:| 
| PAF      | Performance Abnormality Flag| 
| RTT     | Round Trip Time      |   

	

**5.	References-**

*	[wiki](https://wiki.cerner.com/pages/viewpage.action?spaceKey=cernerworks&title=Statistical%20Process%20Control%20(SPC)%20of%20ICA%20RTT%20(Round%20Trip%20Time)%20Data#StatisticalProcessControl(SPC)ofICARTT(RoundTripTime)Data-ICARTTPAFNotifications/HowtoFindICARTTPAFData)
*	[wiki](https://wiki.cerner.com/display/public/reference/Understand+ICA+Round+Trip+Time+Dashboards+in+Lights+On+Network)


**6.	Detailed Requirements-**
    
1.	Research ICA RTT PAF
    
    1.1.	General definitions and applications of ICA RTT and ICA RTT PAF
    
    1.2.	Current thresholds and workflows associated with generating/responding to ICA RTT PAF alerts

2.	Identify sources of ICA RTT PAF data
    
    2.1.1.	Reach out to IBM Streams team for access to Vertica database
    
      2.1.1.1.	Contacts – Adam Splitter, Cory Tenbarge

3.	Investigate the possible ways of extracting ICA RTT PAF data

4.	Develop a design for the integration mechanism
    
    4.1.	Identify the NOC tools that will need access to the data
    
    4.2.	Determine the appropriate thresholds for alerting
    
      4.2.1.	Should be low enough to allow for proactive investigation (i.e. before the client feels the impact)

**7.	Required Details-**
    
*	Data- NA
    
*	Resource Dependency- NA
    
*	Access- NA

**8.	Form / Report Specifications-**

NA

**9.	Testing Considerations-**
    Testing is not required for this project as this is a SPIKE story.

**10.	Appendices / Attachments-**
    
NA




