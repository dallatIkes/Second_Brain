# OCI Introduction

## OCI Architecture

**Region :**  Localized Geographic Area with one or more Availability Domains
**Availability Domain :** One or more fault tolerant data centers (high bandwidth - low latency)
**Fault Domain :** Grouping of hardware and infrastructure (logical data centers)

How to choose a region ?
- Location
- Data Residency and Compliance
- Service Availability

Availability domains are isolated from each other, fault tolerant and unlikely to fail simultaneously because they do note share physical infrastructure. 

Replicate data and applications in different fault domains in different availability domains for redundancy and high availability. Main problem : synchronisation. Solution : Data Guard.

![[Pasted image 20250915002911.png]]

## Identity and Access Management

### IAM Introduction





