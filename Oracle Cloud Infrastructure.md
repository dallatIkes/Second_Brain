[[Oracle Cloud Infrastructure]] (OCI) is [[Oracle]]'s cloud computing platform offering a wide range of [[IaaS|Infrastructure-as-a-Service]] (IaaS) and [[PaaS|Platform-as-a-Service]] (PaaS) services. It's designed to provide the high performance and control of on-premises infrastructure with the flexibility, scalability, and convenience of the public cloud. [[Oracle Cloud Infrastructure|OCI]] is used to build and run diverse applications, including enterprise databases, [[AI]] workloads, and cloud-native applications, across a global network of regions and customer data centers.  

---
# OCI Foundation

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

Role based access service, two key aspects : 
- **AuthN** : Authentification (who are you ?)
- **AuthZ** : Authorization (what are your permissions ?)

**Identity Domain** : logical construct to keep the users in group in order to apply policies. 

![[Pasted image 20250916170117.png]]

### Compartments

Logical construct where you keep your cloud ressources.

Each ressource belongs to a **single** compartment. 
Why ? Controlling access !
Ressources cans interact with other ressources in other compartments.
Ressources can be moved from one compartment to another.
Ressources from multiple regions can be in the same compartment. (They are global)
Compartments can be nested (up to 6 levels)
You can set quotas and budgets on compartments.

Powerful structure for projects **hierarchy** and **design**.

### AuthN and AuthZ

**Principal** : IAM entity that is allowed to interact with [[Oracle Cloud Infrastructure|OCI]] ressources. It can be : 
- IAM Users
- Ressource Principals

A **group** is a collection of users with the same access to ressources.

**AuthN** : are you who you say you are ?
- username / password
- [[API]] Signing Key 
- Auth Tokens (third party [[API]]s)

**AuthZ** : what permissions do you have ? done though **policies** human-readable statement to define granular permissions (it can be attached to a compartment or a tenancy - account).

Syntax : 
```oci
Allow <domain_name>/<group_name> to <verb> <ressource-type> in <location> where <condition>
```

### Tenancy Setup

**Best practices :** 
- don't use the Tenancy Administrator Account for day-to-day operations but rather an [[Oracle Cloud Infrastructure|OCI]]-admin-group with dedicated policies
- create dedicated compartments to isolate ressources
- enforce the use of [[MFA|Multi-Factor Authentification]] (MFA)

## Networking

### VCN Introduction

Virtual Cloud Network : 
- Private Network
- Secure communication
- Lives in [[Oracle Cloud Infrastructure|OCI]] Region
- Highly available

**Communication :**
- Internet Gateway : access the Internet
- NAT Gateway : access the Internet but unidirectional
- Service Gateway : access [[Oracle Cloud Infrastructure|OCI]] public services 
- Dynamic Routing Gateway : Site-to-Site [[VPN]] Connect

### VCN Routing

**Route Tables** used to communicate with : 
- Internet
- On-Premises Network
- Peered VCN
Destination [[CIDR]] block + Route Target

**Peering :**
- Local Peering (same region)
- Remote Peering

Dynamic Routing Gateway (v2) : connect 3+ VCNs

### VCN Security

**Security Lists** : firewall rules applied to all VCNs in a subnet
**Network Security Group (NSG) :** also firewall rules but only specific VCNs

### Load Balancer (reverse proxy)

Achieve High Availability and Scalability

- Layer 7 : [[HTTP]]/[[HTTPS]]
	- Scalable - Flexible/Dynamic shapes
	- higher intelligence : inspects packets
- Layer 3/4 : [[TCP]]/[[UDP]]
	- much faster

## Compute

### Compute Introduction

Provides [[Virtual Machine|VM]] and bare metal servers to meet the application requirements. It ensures scalability, high performance and lower pricing.

- [[Virtual Machine]]
- Bare Metal
- Dedicated Host

### Instance Basics

![[Pasted image 20250916234154.png]]

VNIC : connection to the VCN (private [[Adresse IP|IP Address]])
Remote storage : boot ([[Operating System|OS]] image) and data

Live Migrate the [[Virtual Machine|VM]]s between hosts if the current host fails

### Scaling

**Virtual Scaling :** Scale-up and scale-down instance shape supported. New shape must have same hardware architecture. Downtime required (other host). Good practice : stop instance before resize.

**Auto scaling :** scale-out or scale-in. One [[Virtual Machine|VM]] fails, others keep working. Match traffic demand by adding/removing [[Virtual Machine|VM]]s automatically (write the scaling rules in a Config file).

### [[Oracle]] Container Engine for [[Kubernetes]] (OKE)

[[VM vs Container]]

[[Docker]] - [[Kubernetes]]

Fully managed scalable, and highly available service based on the [[Kubernetes]] engine.
It allows : 
- one click cluster creation
- CLI/[[API]] support
- Support for Arm and [[GPU]] instances
- Auto scaling supports
- Automatic [[Kubernetes]] upgrade
- Self-healing cluster nodes

![[Pasted image 20250917011348.png]]

**Node :** Machine where [[Kubernetes]] is installed
**Pod :** Group of one ore more [[Container|containers]] with shared storage and network ressources + specification file

**Control plane nodes :** make decisions about the cluster (how to schedules, scale, failure, ...)

Two types of clusters : 
- Enhanced Clusters : support all available features
- Basic Clusters : support the core functionality

Two types of nodes :
- Virtual Nodes : [[Serverless]] [[Kubernetes]] experience (only in enhanced clusters)
- Managed Nodes : we are responsible for managing the node, upgrading [[Kubernetes]]...

### [[Container]] workload in [[Oracle Cloud Infrastructure|OCI]]

[[Oracle Cloud Infrastructure|OCI]] [[Container]] instances eliminates operational complexities for users. It takes care of the underlying container runtime and compute ressources. The compute infrastructure provides robust workload isolation for enhanced security.

### [[Serverless]] with [[Oracle]] Functions

![[Pasted image 20250917014749.png]]

Functions-as-a-Service - Event driven architecture - runs in a [[Container]]

How it works ?
- push container to registry
- configure function trigger
- code runs only when triggered
- pays for code execution time only

## Storage

### Storage Introduction

Storage requirements :
- Persistent vs Non-persistent
- What are you storing ?
- Protocol
- Durability (redondance)
- ...

[[Oracle Cloud Infrastructure|OCI]] Storage Service :
- Local NVMe
- Block Volume
- File Storage
- Object Storage

[[Oracle Cloud Infrastructure|OCI]] Data Migration Services :
- Data Transfer Disk
- Data Transfer Appliance

### Object Storage

- Data is managed as object 
- Ideal for unstructured data (logs, videos, images, text files, ...)
- regional, public service
- multiple storage tiers
- private access from [[Oracle Cloud Infrastructure|OCI]] ressources
- advanced capabilities

**Scenarios :**
- Content repository
- unstructured/semi-unstructured data
- big data
- archive/backup

**How does it works ?**
Object : Name + Value (+ metadata)
They are stored in a bucket( unique name in  a tenancy - flat hierarchy)
Namespace : logical entity; top level container for all buckets/objects

**Object Tiers :**
- Standard (hot tier) : critical data to retrieve instantaneously
- Infrequent Access : long term critical data (backups)
- Archive Tier : rarely access this data
Auto-Tiering $\rightarrow$ automatically sets the data object tier

**Life cycle Management :** transfer data from higher cost tiers to lower cost tiers cheaper

**Data Encryption :** by default - cannot be turned off

### Block Volume

Persistant and durable storage

**Tiers :**
- lower cost (e.g. [[Base de données|db]] housing)
- balanced (e.g. boot disk)
- higher performance (most demanding workloads)
- ultra high performance (highest demanding [[IO]] workloads e.g. [[Modèle relationnel|relational db]])
Auto-Tune Performance

Encryption

Resizing (while running)

Replication of Block Volumes

Volume Groups : group together multiple block volumes

### File Storage

Hierarchical Collection of documents organized into named directories 

Distributed File System : NFS ([[Linux]]) - SMB([[Windows]])

- Shared storage for compute instances
- Supports NFSv3 distributed file stystem
- Data protection : Snapshots
- Security : Data-at-rest and in-transit encryption

## Security

### Security Introduction

Shared Security Model : security responsibilities are shared between the client and the cloud provider.

- Infrastructure Protection (firewalls)
- IAM 
- OS and Workload Protection ([[Virtual Machine|VM]]s)
- Data Protection
- Detection and Remediation (management & intelligence)

### Cloud Guard

Help to monitor and identify security issues and automatically fix them.

#Scenario : problem detected, create an issue, it can trigger a cloud event, if a policy has been configured in the Cloud Guard, a respond is emitted. 

### Security Zones and Security Advisor

**Security Zones :** container with policies
**Security Advisor :** combination service (cloud guard, security zones, ...)

### Encryption Basics

plain text $\rightarrow$ cipher (encrypted) text
key pairs

Encryption at rest : stored data
Encryption in-transit : data transferred (e.g. [[HTTPS]])

#Reminder : [[Cryptographie|Cryptography]]

Hardware Security Module : physical computing device used to manage digital keys and performs [[Cryptographie|cryptographic]] functions.

### Vault

Centrally Managed Keys and Credentials (not expose them in code or config files)

- Software Protection (in a Server, can be exported)
- Hardware Protection (HSM : cannot be exported)

**Envelope Encryption :** Data Key used to encrypt data is encrypted by the Master Key

![[Pasted image 20250918115407.png]]

## Governance and Administration

## Pricing

- Pay as you go (PAYG)
- Annual Universal Credits
- Bring Your Own License (BYOL)

Pricing Factors : 
- Ressource size
- Data transfer
- Ressource Type
- ...

### Cost Management

Budget : track the costs and set up alerts
Cost Analysis : Usage Reports
Compartment Quotas : set up limits to prevent miss uses or go over budget

### Tagging

Key-Value Pair used to better organize ressources

- Free-form Tags
- Defined Tags (contained in namespaces, defined schema, secured with policies)

### Support Reward

Program to save costs according to the services usage


--- 
# OCI Generative [[AI]]

## Fundamentals of [[Large Language Models]] 

### Introduction to [[Large Language Models|LLMs]] 

$\rightarrow$ go see the [[Large Language Models]] page

### [[Large Language Models|LLMs]] Architectures

Multiple architectures focused on encoding and decoding all built on the Transformer Architecture.

![[Pasted image 20250918224140.png]]

**Encoders :** embed text (converting a sequence of words into vectors). The vectors can be used for classification or vector search.

**Decoders :** take a sequence of tokens and output the next (more probable) token. (Always one token at a time).

**Encoder-decoder :** the output of the encoder is the input of the decoder + self referential loop (e.g. translation)

### Prompting and Prompt Engineering

We can affect the probability distribution of the vocabulary words in 2 ways : 
- Prompting
- Training

**Prompting :** changing the text input given to the [[Large Language Models|LLM]] 
**Prompt Engineering :** process of iteratively refining a prompt aiming at a particular distribution

**in-context learning :** prompting an [[Large Language Models|LLM]] with instructions and or demonstrations of the task it is meant to complete
**k-shot prompting :** explicitly providing $k$ examples of the intended task in the prompt
```c
Translate English to French :    // task description
sea otter => loutre de mer       // example
peppermint => menthe poivrée     // example
plus girafe => girafe peluche    // example
cheese =>                        // prompt
```
**Few-shot prompting** is widely believed to improve results over **0-shot prompting**.

**Chain-of-Thought prompting :** prompt to emit intermediate reasoning steps

**Least-to-most prompting :** prompt the model to solve a problem and to use its solution to solve another more difficult problem

**Step-Back prompting :** prompt the model to identify high-level concepts pertinent to a specific task

### Issues with prompting

**Prompt injection (jailbreaking) :** prompt the model to make it behave contrary to deployment expectations

### Training

Sometimes, prompting is not enough, you need to enhance its performance outside of the domain/subject-area it was trained on.

**Fine-tuning :** classical [[Machine Leaning]] training where we change all the parameters (very expensive!)
**Parameter Efficient Fine-tuning :** we keep the parameters of the model fixed and add new ones
**Soft prompting :** add parameters to the prompt (learnable prompt)
**Continual pre-training :** like fin-tuning but without labeled data

### Decoding

**Greedy decoding :** pick the highest probability word at each step
**Non-Deterministic decoding :** pick randomly among high probability candidates at each step

**Temperature :** (hyper) parameter that modulates the distribution over vocabulary (low temperature : the distribution is peaked - high temperature : the distribution in flattened)

- Scientific exact result $\rightarrow$ greedy low temperature decoding
- Writing a story $\rightarrow$ non-deterministic high temperature decoding
### Hallucination

**Hallucination :** generated text unsupported by any of the data fed to the model

No known methods to reduce hallucinations in a model but there are best practices like providing examples.

**Grounded :** generated text supporting a document

### [[Large Language Models||LLM]] Applications

**Retrieval Augmented Generation (RAG) :** the model has access to support documents for a query (claimed to reduce hallucination)

**Code Models :** [[Large Language Models|LLMs]] trained on code, comments and documentation (better to patch bugs than to write code from scratch)

**Multi-Modal :** models trained on multiple modalities (e.g. language and images)

**Language Agents :** models intended for sequential decision making (e.g. playing chess)

## [[Oracle Cloud Infrastructure|OCI]] Generative [[AI]] Service

### [[Oracle Cloud Infrastructure|OCI]] Generative [[AI]]

Fully Managed service providing a set of customizable [[Large Language Models]] via a single [[API]] to build generative [[AI]] applications.

- High performing pretrained foundational models from Meta and Cohere
- Flexible Fine-tuning with your own data set
- Dedicated [[AI]] clusters ([[GPU]])



---
# OCI [[Data Science]] 















