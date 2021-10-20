---
abbrev: iiot-framework
docname: draft-iotops-km-iiot-frwk-latest
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
  city: Santa Clara, CA 95050
  country: United States of America
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
  SURV:
    DOI.10.1109/SURV.2012.071812.00124
  ISA95:
    title: "ANSI/ISA-95.00.01-2010 (IEC 62264-1 Mod) Enterprise-Control System Integration - Part 1: Models and Terminology"
    target: https://www.isa.org/standards-and-publications/isa-standards/isa-standards-committees/isa95

  IIC_TALK:
    title: "Overview of IIC – Building the IIoT Ecosystem"
    author:
       ins: W. William Diab
       name: Wael William Diab
       org: Industrial Internet Consortium
    target: https://github.com/iot-dir/Meetings/blob/main/20211012/slides/Diab_IIC_Overview_for_IETF_1021_rev2.pdf
    date: 2021-10-12

​--- abstract

Industry control networks host a diverse set of non-internet protocols supporting Industrial-IoT and legacy device connections. The integration between traditional information technology (IT) and operational technology (OT) so far has centered around collection of real-time data from devices in OT environment for consumption within the enterprise IT networks. However, improvements in process control and automation require a far better interworking between the OT and IT applications. This document provides an overview of a reference framework for integrated industry networks. It specifically focuses on identifying the differences between the IT and OT networks and suggests the use of IETF technologies to bridge those differences.

​--- middle

# Introduction {#intro}

There is a very little cross-over between the network technologies used in the OT and IT environment. The OT networks are responsible for atomation and process control on premises such as factory floors, manfacturing plants, power grids, oil & gas industry, etc. In contrast, IT networks traditionally facilitated business applications based on data received from OT applications. With increased atomation, and growing demand for remote operations, it is imminent that the two technology domains need to interwork seemlessly and reliably.

Since there is little coordination between industrial networks and IETF technologies, the evolution paths are different and as a result, current IETF technologies and protocols are not well adapted in industrial networks. Industrial systems and applications are becoming increasingly complex and proprietory as emerging use cases require a higher integration of OT-IT functions.

The OT networks are often tied to a set of non-internet protocols such as
Modbus, Profibus, CANbus, Profinet, etc. There are more than 100 different protocols each with it's own packet format and are used  in the industry.
On the other side inventory management, analytics, monitoring, supply chain and simulation software are part of IT and use IP based technologies.

> Note: use IETF technology (instead of IP-based) as a more inclusive term.

No two industry sectors are similar and present different requirements and challenges on the networks. The processes, control operations, environmental conditions, frequency and type data collection vary across each sector.

> Todo: Add examples from petrochem or mining plant, manufacturing and transportation. Refer to IIC case studies.

This document provides a  framework for Industrial Networks and  discusses details of integration of process control, monitoring and operations with IT. It proposes (a) an integrated industrial network stack that would support functions and capabilities from both OT and IT systems, (b) a structured deployment considerations, (c) alignment and coordination across stakeholders from other consortia and SDOs.

Establishing a baseline framework helps in identifying components for integrated industrial networks.

# Terminology

* Industrial Control Networks:
The indutrial control networks are interconnection of equipments used for the operation, control or monitoring of machines in the industry environment. It involves different level of communications - between fieldbus devices, digital controllers and software applications

* Industry Automation:
Mechansims that enable  machine to machine communication by use of technologies that enable automatic control and operation of industrial devices and  processes leading to minimizing human intervention.

* Control Loop:

* Feedback Control Loop:

* Programmable logic controllers (PLC):
  Industrial computers/servers for the control of manufacturing processes such as assembly lines .
* Supervisory Control and Data Acquisition (SCADA) i
  Software System to control industrial processes and collect and manage data.

* Distributed Control Systems (DCS):
  Systems of sensors and controllers that are distributed throughout a plant.

* Manufacturing Execution System (MES):
  Systems that connect production equipment across the factory floor, or multiple plants or sites
* Fieldbus Devices:
  Operational Technology field devices include valves, transmitters, switches and actuators
   etc.
* Integrated Industrial Network (IIN):
  The term introduced in this document to represent a converged view of OT and IT networks.

## Acronymns
* HMI: Human Machine Interface
* MES: Manufacturing Execution System
* IIN: Integrated Industrial Network
* IIC: Industrial Internet Consortium

# High Level Considerations

Framework should provide a clear understanding of the functional and operational requirements. It will require several components that together fulfill the needs for both IT and OT applications. Integrated Industrial Network (IIN) Framework needs to meet and adapt to evolving deployment strategies that include cloud, edge technologies. Finally, a key consideration is close coordination with the stakeholders. They are the domain experts from their respective fields and are more aware of technical challenges.

## Integrated Industrial Network Stack

Industrial Networks are a combination of technologies that provide capability for the delivery of process control data to/from (and across) the machines and sensors to different controllers and other application specifc servers. Thus, the IIN stack should combine OT and IT functions.

The focus of OT network protocols is on efficiency, utilization, consistency, continuity
and safety

### OT Network Protocols
The OT networks were originally designed for small scale operations set of non-internet protocols such as
Modbus, Profibus, CANbus, Profinet, etc. There are more than 100 different protocols each with it's own packet format and are used  in the industry.
On the other side inventory management, analytics, monitoring, supply chain and simulation software are part of IT and use IP based technologies.

### IETF Technologies

### Challenges
#The scope of this document should be connectivity related convergence of IT and OT. 

Therefore, the interfaces between business layer and process control layer are captured in detail as they are more interesting (or relevant) for inter-operation discussions. The document specifcally focuses on the new emerging trends that could potentially impose new connectivity requirements. Key emerging trends discussed are: (a) device to cloud mechanisms, (b) virtualization, (c) high-volume data emission, (d) location awareness, and (e) industry device security enhancements.

## Deployment Considerations
Logically, the  industrial networks are under a single administrative control or  a limited group of administrators. They are expected to extend across different geographies and over a range of distances to meet low-level requirements.

### OT Network Designs

## Alignment with stakeholders

The paradigms of networking in OT are quite different that IP based best-effort networking protocols. When it is not possible to get contributors directly from the industry sectors using OT, coordination with well-established consortia where industrial networking is discussed may be utilized.
For example, a {{IIC_TALK}} provided overview of IIC activities and
TODO: Next steps.

# Industrial Network Reference Architecture {#arch}

 The following reference  industrial network will be used to provide structure to the discussion. In the Fig. {{indusarch}} below, a hierarchy of communications is shown. At the lowest level, PLCs operate and control field devices; above that Human Machine Interface
 (HMI) interconnects with different PLCs to program and control underlying field devices. HMI itself, sends data up to applications for consumption in that industry vertical.

~~~~~~~~~~
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

~~~~~~~~~~
{: #indusarch title="Hierarchy of Functions Industrial Control Networks"}



Unlike commercial networks that uniformly run IP protocols, the communication links run different protocols at along the different level of the hierarchy. One of the key requirement from new industrial applications is the integration of different types of communication protocols including Modbus, Profinet, Profibus, ControlNet, CANOpen etc.

A vertically integration system involves a network between the external business applications and higher controllers (for e.g. SCADA, HMI, or system integrators) is IP based. The second level of networks between  the controllers can be either IP or non-IP (Profibus, BACNet, etc.). The lowest field-level networks between industrial controllers and field-level may be any of the fieldbus or device control protocols (More details of the industry networks can be found in  {{SURV}}).

# IIoT Framework

Traditionally, OT and IT experts have focussed on different concerns. On a production floor or with OT, the focus is generally on no congestion, lossless reliable transmission, and real-time or deterministic communication. Quality of manufactured goods, and efficiency of processes is also an important concern for OT experts.

On the IT side, concerns are same as those in enterprise of campus networks, i.e., scalability, security, interoperability, compute and storage capability and well-defined maitenance procedures to reduce downtime and outages.

Now, with Industry 4.0 initiatives such as smart factory and smart manufacturing), these concerns are beginning to overlap, i.e. scalability, security, interoperability, maintenance are becoming common concerns for both OT and IT domains of industry verticals.

> Editor's Note: Should we expand on how the above mentioned are new concerns - scale, security, interoperability?

# Evolution of Requirements (Tentative)

 Multi-disciplinary approach to automation in which different processes are fully integrated. See


(a) device to cloud mechanisms, (b) virtualization, (c) high-volume data emission, (d) location awareness, and (e) industry device security enhancements.

## Device to Cloud Mechansims
Perimeter of device control is expanding from factory floors to the cloud. It is anticipated that Industrial IoT controls when extended to the cloud or edge compute platforms will offer better integration with sophisticated business logic application architectures.

Since these networks are not equipped with compute intensive servers. Now extending the communication to the edge and cloud nodes increases the distance requiring traditional L2 networks to be adopted to L3 network designs.

### Traditional Network and Device Access Scope
Traditional MES run on internal infrastructure with legacy workstations and network. There is a conservative approach to upgrading any aspect of the infrastructure - due to the cost and effort invovled.

### New Expectations
Cloudification of upper tiers of automation pyramid ISA-95 {{ISA95}} standard

~~~~~~~~~~ drawing
            /\
           /L4\         'ERP'- Business planning and logistics
          /----\
         /  L3  \       'MES'- Manufacturing Ops & Mgmt
        /--------\
       /    L2    \     'SCADA'- Monitoring & Supervisory
      /------------\
     /      L1      \   'PLC' - Sensing and Control
    /----------------\
   /        L0        \  Sensors, Motors, actuators - Production process
  /____________________\
~~~~~~~~~~
{: #Automation title="ISA 95 model of Automation Pyramid"}

Higher powered compute platforms are offered in the cloud.

## Virtualization
New aspect of industry automation is virtualization of PLCs themselves. The vision is to
## Device Identity and Address

Shorter addresses are inherent to industry control systems to provide implicit determinism. For this purpose, the industrial networks use fieldbus interface with the controllers.

### Current State

### Implications of Virtualization
Functionally, how IIoT will work is not a challenge. From communications standpoint there are 3 key implications
 1. That the PLCs are no longer one-hop away: - it is important to track the path traversed, accuracy and feedback is necessary.
 2.  Security implications

# High-volume Data Emission
Industry verticals keep data and control on the manufacturing floor, on a closed system. There is no easy way to forward this data to enterprise level software. On premise micro data centers or edge computing are new infrastructure pieces that wil impact the design of current industrial networks.

## Virtualization



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

# Automation

There are several obvious benefits of automation that can be found in various automation projects as primary positive results. Among others, they include:

## Resource Efficiency

## Higher Accuracy

## Increased focus on core



competencies # Improved productivity # Better compliance # Creating New

jobs # Reducing Employee turnover. Three types of automation in production

can be distinguished: 1. Fixed automation, 2. Programmable automation, and 3.

Flexible automation.

## Digital Twin

A digital twin is a virtual 3D
representation of the real world. It
can show physical objects, processes,
relationships, and behaviours – and it
can represent them as they are now,
as they were in the past or will be in
the years ahead.

## Limited Domain Network Inspired Architecture
Industry networks can be designed using LDN {{LDN}} framework.

# IANA Considerations

This document requires no actions from IANA.

# Security Considerations

This document introduces no new security issues.

# Acknowledgements


--- back

