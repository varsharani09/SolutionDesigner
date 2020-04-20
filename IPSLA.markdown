---
layout: page
title: IPSLA
permalink: /ipsla/
---

**Goal:** Gather IPSLA metrics, node metrics and interface metrics from Kafka and enrich them to make them more understandable and readable. The objective is to enrich them so that they can be consumed by data scientists and data analysts and perform data analytics on the performance metrics.

**Metrics enriched at present:**
**Interface type:**

1. Octets

    * ifInOctets

    * ifOutOctets

    * ifHCInOctets

    * ifHCOutOctets

    Using the above 4 fields and the speed metrics we have also calculated the below 4 fields:

    * inOctetUtilization%

    * outOctetUtilization%

    * highInOctetUtilization%

    * highOutOctetUtilization%

2. Discards

    * ifInDiscards

    * ifOutDiscards

3. Errors

    * ifInErrors
    
    * ifOutErrors

4. Speeds

    * ifSpeed
    
    * ifHighSpeed
    
**CPU and Memory Type/Node:**

* avgBusy5minUtilization%
    
* ciscoMemoryPoolFreeInMBs
    
* ciscoMemoryPoolMaxInMBs
    
* ciscoMemoryPoolUsedInMBs
    
* memoryPoolFree%
    
* memoryPoolUsed%
    
* totalMemoryInMBs
    
* cpuUtilization%

 **IPSLA/Generic type**

1. jitterRTTSumInMillisecond - This is a new field added in addition to jitterRTTSum just to help the consumers know what is it unit. Both jitterRTTSumInMillisecond and jitterRTTSum have the same value.



**Solution:** Formulae to calculate all the metrics mentioned above is present in the excel sheet attached. The metrics are of String, integer, gauge and counter type. Though its easy to enrich and consume the first three types, counter type is tricky. Counter metrics are of interface metric type and include Octets, Discards and Errors, these are interface performance metrics. Characteristic of a counter metric is that its ever increasing until it reaches it max cap value depending on whether its a Counter(32-bits) or a High Counter(64-bits). Once a Counter metric reaches its cap value counter wrap which means that the value gets dropped to a smaller value, this sudden drop or the counter wrap makes these fields hard to plot and hard to assess. To counter this situation 2-phase adjustment technique is used as below to transform the metric into a new field which will be smaller in size and more comprehensible:

Current Polled Value = CPV
Previous Polled Value = PPV
Current Polled Time = CPT
Previous Polled Time = PPT
delta_value = CPV - PPV, only when both are not null.
delta_time = CPT - PPT, this can never be null.


Step1: if delta_value < 0, start 2 phase adjustment of delta
Step2: Try 32 bits adjustment first
delta_value = delta_value + 2 ** 32
Step3: if delta is still negative then try 64 bits adjustment
if delta_value < 0
delta_value = delta_value - 2 ** 32 + 2 ** 64
Step4: Convert time delta in seconds
delta_time = (CPT - PPT)/1000
Step5: if delta_time is positive its valid but for 0 delta_time or negative delta_time set the transformed field to 0
*metric's transformed value = delta_value/delta_time*

ifSpeed(32-bits) and ifHighSpeed(64-bits) are bandwidth estimators and are used to calculate the Utilization percent values.
From the above derived transformed fields we can calculate bandwidth utilization% values, by diving the transformed value with the speed metrics, 32 or 64 bits depending on the counter type.



**Future usage:** The above implementation is performed in a Logstash config file and for any other metric field the same config can be used. Please make sure to follow similar process to transform counter based interface type metrics. For gauge, String and Integer fields rules may differ.

Link to the excel sheet: [Ipsla_CPU_Memory_Interface](https://wiki.cerner.com/download/attachments/2266564661/Ipsla_CPU_Memory_Interface.xlsx?version=1&modificationDate=1586453604000&api=v2)
