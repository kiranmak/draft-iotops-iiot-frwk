---
abbrev: iiot-framework
docname: draft-iotops-indnet-framework-00
title: Framework For Industrial Networks 
date:  false
category: info

ipr: trust200902
area: IOTOPS
workgroup: Independent Submission
keyword: Internet-Draft

stand_alone: yes
pi: [toc, sortrefs, symrefs]

author:
-
  ins: K. Makhijani
  name: Kiran Makhijani
  org: Futurewei
  email: kiran.ietf@gmail.com
-
  ins: L. Dong
  name: Lijun Dong
  org: Futurewei
  street: Central Expy
  city: Santa Clara, CA 95050
  country: United States of America
  email: lijun.dong@futurewei.com

informative:

  LDN: RFC8799
  DETNET-DP: RFC8939
  DETNET-ARCH: RFC8655
  SCHC: RFC8724
  ROHC: RFC4995
  FlexIP: I-D.moskowitz-flexip-addressing
  Flexible_IP: I-D.jia-flex-ip-address-structure
  CHALLEN: I-D.jia-intarea-scenarios-problems-addressing
  SOIP: I-D.jiang-service-oriented-ip
  FHE:  I-D.jiang-asymmetric-ipv6

  IEEE802.1TSNTG:
    target: https://1.ieee802.org/tsn
    title: IEEE, "Time-Sensitive Networking (TSN) Task Group"
    date: 2018
  
  SURV: 
    DOI.10.1109/SURV.2012.071812.00124

--- abstract

Industry Control Networks host a diverse set of non-internet protocols for different purposes. Even though they operate in a controlled environment, one end of industrial control applications run over internet technologies (IT) and another over operational technology (OT) protocols.  This memo  discusses the challenges and requirements relating to converegence of OT and IT networks. 
 One particular problem in convergence is figuring out reachability between the these networks.

--- middle

# Introduction {#intro}

An industry control network interconnects devices used to operate, control and monitor  physical equipment in industrial environments. These networks are increasingly becoming complex as the emphasis on convergence of Operational Technologies (OT) and Information Technologies (IT) grows to meet the business objectives. The OT networks are often tied to set of non-internet protocols such as 
Modbus, Profibus, CANbus, Profinet, etc. There are more than 100 different protocols each with it's own packet format and are used  in the industry. 
On the other side inventory management, supply chain and simulation software are IT based. 

This document provides a  framework for Industrial Networks. The scope includes details of their operations, processes, control and integration with IT.
   Industrial Networks can be seen as combination of technologies which provides a capability for the delivery of data flows between machines and sensors on the floors to different controllers and other application specifc servers. 
   
   Logically, the  industrial networks are under a single administrative control or  a limited group of administrators. They are expected to extend across different geographies and over a range of distances to meet low-level requirements.
The scope of process and operations refer to 
   The framework in this document serves as a generalized baseline of well-established network architecture relating to  different verticals and mechanisms deployed for extending those to the cloud-based applications. The processes and operations across verticals are inter-connected. It includes manufacturing, energy, transportation, 
Insights and Federated Analytics
Abstracting Hardware elements to software elements.
   n of IT and OT.

feedback and control loops throughout distributed manufacturing infrastructures.

# Terminology

* Industrial Control Networks:
The indutrial control networks are interconnection of equipments used for the operation, control or monitoring of machines in the industry environment. It involves different level of communications - between fieldbus devices, digital controllers and software applications

* Industry Automation: 
Mechansims that enable  machine to machine communication by use of technologies that enable automatic control and operation of industrial devices and  processes leading to minimizing human intervention.

* Control Loop:

* Feedback Control Loop:


## Acronymns
* HMI: Human Machine Interface



# Industrial Network Reference Architecture {#arch}

In the scope of this document the following reference  industrial network will be used to provide structure to the discussion. In the Fig. {{indusarch}} below, a hierarchy of communications is shown. At the lowest level, PLCs operate and control field devices; above that Human Machine Interface
 (HMI) interconnects with different PLCs to program and control underlying field devices. HMI itself, sends data up to applications for consumption in that industry vertical.


          +-+-+-+-+-+-+
       ^  | Data Apps |....             External business logic network
       :  +-+-+-+-+-+-+   :
       :        |         : 
       v  +-+-+-+-+-+-+  +-+-+-+-+--+
          | vendor A  |  |vendor B  |     Interconnection of 
          | controller|  |controller|     controllers (system integrators)
       ^  +-+-+-+-+-+-+  +-+-+-+-+-+    
       :       |         |          
       :   +-+-+-+-+  +-+-++-+
       :   | Net X |  | Net Y|
       v   | PLCs  |  | PLCs |--+        device-controllers
       ^   +-+-+-+-+  +-+-+--+  |
       :      |        |        |
       :   +-+-+    +-+-+    +-+-+
       v   |   |    |   |    |   |   Field level devices 
           +-+-+    +-+-+    +-+-+
{: #indusarch title="Hierarchy of Functions Industrial Control Networks"}



Unlike commercial networks that uniformly run IP protocols, the communication links run different protocols at along the different level of the hierarchy. One of the key requirement from new industrial applications is the integration of different types of communication protocols including Modbus, Profinet, Profibus, ControlNet, CANOpen etc.  

A vertically integration system involves a network between the external business applications and higher controllers (for e.g. SCADA, HMI, or system integrators) is IP based. The second level of networks between  the controllers can be either IP or non-IP (Profibus, BACNet, etc.). The lowest field-level networks between industrial controllers and field-level may be any of the fieldbus or device control protocols (More details of the industry networks can be found in  {{SURV}}).

# Framework
The production network is part of the production process and thus lies at the heart of every manufacturing company.
# Reference usage scenario
Demonstration of a industrial network data flow on a production floor.


# Requirement Challenges

## Cloud to Device Connectivity
  The industry control networks can be extended to cloud or edge compute platforms. Since these networks are not equipped with compute intensive servers. Now extending the communication to the edge and cloud nodes increases the distance requiring traditional L2 networks to be adopted to L3 network designs. 

 Design decisions will require to choose different transit strategies (this maybe layer 1, 2, 3 technologies or even network slices). It also influence the security policies.

## Device Identity and Address

Shorter addresses are inherent to industry control systems to provide implicit determinism. For this purpose, the industrial networks use fieldbus interface with the controllers.

# Applying Limited Domain Network Taxonomy


# Factors Driving Network Layer Interrations

## Background
Legacy architectures on factory floors use a condenced OSI stack model From smaller address of legacy devices to IT based applications with IP address.

~~~~~
(OT-Address )--->(Industry Control)--->(IP-Address) 
(control dev)    (   network      )    (application)
~~~~~

## OT/IT Convergence 
Most of the factory floors are not equipped with IT servers to perform compute intensive tasks. Yet an IP-based device need to connect with non-IP interface to control those devices.
Note: this hypothesis is being challenged.
Often real-time response is necessary for example, in closed-loop control systems direct communication is desired to avoid any additional packet processing delay or overheades at the source and destination gateways, equipping IP to all OT devices and abandoning the existing investment and depolyment could result in the following obvious problems.


  * Many of the standard IP based protocols maybe too much overhead for OT devices.
  * Cannot preserve communication characteristics of devices (different device addressing scheme, realtime, IRT, message identifiers, Bus-like properties).
  * It relies heavily on hierarchy network stack (network layer, transport layer, application), where as OT devices do not have any, they generally operate at data link layer or below.


## Data oriented networking
Industry verticals keep data and control on the manufacturing floor, on a closed system. There is no easy way to forward this data to enterprise level software. On premise micro data centers or edge computing are new infrastructure pieces that wil impact the design of current industrial networks. 

## Virtualization
Traditional Industry control infrastructure is not virtualized. Virtualization will enable deployment of new functionality in a flexible manner.  

- Virtual PLCs are considered an important component functionality customization of digital-twin realization.
- virtualization enables edge and cloud native computing by moving and instantiating workflows at different locations.

Implications that PLCs are no longer one-hop away.


## Short Device Addressing
Shorter addresses are inherent to industry control systems to provide implicit determinism.

Note: The motivation for short address is to preseve the legacy attributes of fieldbus control devices. It is not related low-power or resource constraints.

A large volume of the messages are of sizes shorter than the size of IP headers (v4, v6) themselves. The header tax will be very high over industry control networks.


## Network Layer Adoption
Challenge of Industrial network device address is that it  communicates to a physical device address. Traditionally, in a limited environment there was no need for network layer or expressing network specific service, access control.

- If a sensor is broken, it will require reprogramming of controller and re-aligning with the new address. The benefit of network layer, removes this restriction. 
- Note that, using IP stack is not suitable because these devices perform specific functions and any overhead in transport or large addressing can add to processing delays.
- Several other IP suite protocols such as device discovery should be revisited.
  
## Interoperability with IP-world machines

To develop further on different type of address format support. From smaller address of legacy devices to IT based applications with IP address.

~~~~~
(OT-Address )--->(Industry Control)--->(IP-Address) 
(control dev)    (   network      )    (application)
~~~~~

Preferably allow OT devices to understand IP-addresses for the servers they connect to.


# Relationship with  Activities in IETF {#relevance}

## Deterministic Networks (DetNet WG)
The Deterministic Networking (DetNet) {{DETNET-ARCH}} is working on using IP for long-range connectivity with  bounded latency in industry control networks . Its data plane {{DETNET-DP}} takes care of forwarding aspects and most close to Industry control networks but the focus is on the controlled latency, low packet loss & delay variation, and high reliability functions. Not dealing with interconnection of devices.

In layer 2 domain, similar functionalty is convered by TSN Ethernet {{IEEE802.1TSNTG}}.

## IoT OPS
IoT operations group discusses device security, privacy, and bootstrapping and device onboarding concepts. Among the device provisioning one of the object is network identifier. We understand that the IoT OPs does not exclude evaluation of industry IoT or control devices requirements.
Given the specific functions described above it maybe necessary to configure more than an identifier, i.e. server or controller information or specific address scope and structure.


## LPWAN
The LPWAN has focussed on low-power and constrained devices. There are compression related approaches that may apply are {{SCHC}} or {{ROHC}}.
To be evaluated for process control devices.

## Recent Addressing related work

Some of the work initiated on the addressing include solutions
such as {{FlexIP}}, {{Flexible_IP}}, {{FHE}}, and {{SOIP}}.
 
Recently, a broader area of problem statement and challenges in {{CHALLEN}}.


 

#IANA Considerations

This document requires no actions from IANA.

#Security Considerations

This document introduces no new security issues.

#Acknowledgements


--- back

