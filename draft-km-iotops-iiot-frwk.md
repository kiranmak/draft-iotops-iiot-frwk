---
abbrev: iiot-framework
docname: draft-km-iotops-iiot-frwk-latest
title: Framework For Integrated Industrial Networks
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
  city: Santa Clara, CA 95050
  country: United States of America
  email: lijun.dong@futurewei.com

informative:

  DETNET: RFC8655
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

  OPC:
    title: Open Platform Communications
    target: https://opcfoundation.org

  IIC:
    title: Industry IoT Consortium
    target: https://www.iiconsortium.org

  OPC_INFO:
   title: "OPC-UA Information Model Specifications"
   target: https://opcfoundation.org/developer-tools/specifications-opc-ua-information-models

  VPLC_CONV: DOI.10.1109/LES.2016.2608418

  VPLC_IIC:
   title: Virtualized Programmable Logic Controllers. An Industrial Internet Consortium Tech Brief
   target: https://www.iiconsortium.org/pdf/IIC-Edge-vPLC-Tech-Brief-20210907.pdf
   date: 2021-09-07
   author:
    -
      org: Huawei Tech
      name: David Lou
    -
      name: Ulrich Graf
      org: Huawei Tech.
    -
      name: Mitch Tseng
      org: TSENG InfoServ, LLC

  ETSI_GS_NFV_003:
   title: "Network Functions Virtualization (NFV) Architectural Framework"
   date: 2017

--- abstract

Industry control networks host a diverse set of non-internet protocols supporting Industrial-IoT and legacy device connections. These networks are physically separated from the enterprise networks and have been slow to adopt the virtualization technologies. Virtualization is necessary to remove the boundaries between the enterprise and process control networks. This document specifies a framework for the converged industrial network. Specifically, it focuses on the virtual PLC scenario. It covers transition technologies required for the convergence of industrial devices with the enterprise application endpoints.

--- middle

# Introduction {#intro}

There is a little cross-over between the network technologies used in the Operational Technology (OT)
and Information Technology (IT) environments as the architecture of industrial networks has evolved independently from the IT networks.
While industrial networks focussed on deterministic communication, safety, and reliability of process control, they have trailed behind in the adoption of virtualization capabilities. The leading vision of industry automation heavily relies on compute and data intensive services.
Although virtualization of SCADA and other systems (HMI, MES, Historian etc.) has happened, the low level PLCs have remained on the factory floor. Virtualization of PLC is a  topic of great interest for fully automated and remote operations in the manufacturing and similar process control industry because it allows direct control of low-level processes from the applications.

There are two primary challenges for PLC virtualization. First one being support for real-time or deterministic functionality on the nodes where these PLC software will reside; secondly a distributed converged network architecture that provides movement of data from devices, sensors and actuators with the same pre-defined latency and safety artifacts.

This document presents the baseline industrial architecture to demonstrate that
the well-established hierarchical architecture poses difficulty for the adoption of
virtualization in the industrial networks.
The scope of the document is primarily on the network-layer technologies that provide basic
functionality for enabling virtualization capabilities both at the endpoint and network level.


The architectural components in this document concern with the
identification of requirements to be met when introducing virtualized PLC,
and in doing so, arrive at a converged industrial network architecture
which supports emerging trends better.
In comparison to the current IP architectures, industrial networks
are required to support coexistence of several industrial protocols and the converged architecture must
support existing mechanisms.

This document discusses those requirements, and proposes a path to converged industrial networking.

# Terminology

{: vspace="0"}
Industrial Control Networks:
 : The industrial control networks are interconnection of equipments used for the operation,
 control or monitoring of machines in the industry environment. It involves different level
 of communications - between field bus devices, digital controllers and software applications

Industry Automation:
 : Mechanisms that enable  machine to machine communication by use of technologies that enable
 automatic control and operation of industrial devices and  processes leading to minimizing human intervention.

Control Loop:
: Todo

Feedback Control Loop:
: Todo

Programmable logic controllers (PLC):
 : Industrial computers/servers for the control of manufacturing processes such as assembly lines.

Supervisory Control and Data Acquisition (SCADA):
 : Software System to control industrial processes and collect and manage data.

Distributed Control Systems (DCS):
: Systems of sensors and controllers that are distributed throughout a plant.

Manufacturing Execution System (MES):
: Systems that connect production equipment across the factory floor, or multiple plants or sites.

Fieldbus Devices:
: Operational Technology field devices include valves, transmitters, switches and actuators etc.

Integrated Industrial Network (IIN):
  : The term introduced in this document to represent a converged view of OT and IT networks.

## Acronyms
* HMI: Human Machine Interface
* MES: Manufacturing Execution System
* CIN: Converged Industrial Network
* IIC: Industrial Internet Consortium

# Architecture
This section discusses the baseline architecture and corresponding design choices made for inter-operation between the enterprise applications and factory floors.

##  Industrial Network Architecture

The physical network architecture for process control and operations centric networks  as shown in {{indusarch}} is rigidly hierarchical.  Note that this figure is over-simplified and in general, each level will have additional hierarchies. For example, when a PLC controlling certain fieldbus devices over ModBus, needs control from another PLC controller say running ProfiNet protocol, a protocol translation gateway is needed. They may also require intermediate network switches to extend connectivity on the factory floor. Similarly, system integrators also need translation gateways for different protocols and additional mechanisms to traffic flow across different switches.

Moreover, communication between the zones levels (see {{Appendix}}) is complex. Among the three zones, Manufacturing, IDMZ and Enterprise, the enterprise network is all IP where as manufacturing and IDMZ network on factory floor are a combination of IP and Industrial protocols. IP switches or routers are used in manufacturing-zone when there is need to extend the network across different cells on factory floors. There are a large number of IP based firewalls and  gateways that perform translation in IDMZ but are required to look at transport payload to determine the industrial protocols and corresponding matching rules.

Factory floor devices do not depend on IP. The PLCs can be instructed or automated to send and receive commands from the I/O or fieldbus devices. The data generated by sensors is captured by industry control systems (SCADA, HMI, MES).
Both DCS and SCADA systems collect data from process instruments and respond with  commands to the actuators. These systems control several process control loop instances simultaneously to handle complex processes. These types of systems were built using proprietary hardware and software, operating in its own zone without additional connectivity. Operators had to work from centralized control room because these systems did not support remote access. The best practices for data delivery to other systems was in the form of reports, which caused significant time lag.

~~~~ drawing
          +-+-+-+-+-+-+
       ^  | Data Apps |    External business logic network
       :  +-+-+-+-+-+-+        (L5)
       :    ||     ||
       v  +-+-+  +-+-+
          |IDS|  |FW |     Translation gateways and firewalls
       ^  +-+-+  +-+-+ -----+  (L4)
       :     |              |
       v  +-+-+-+-+-+-+  +-+-+-+-+--+
          | vendor A  |  |vendor B  |  Interconnection of
          | controller|  |controller|  controllers
       ^  +-+-+-+-+-+-+  +-+-+-+-+-+-      (L2-L3)
       :       |         |
       :   +-+-+-+-+  +-+-++-+
       :   | Net X |  | Net Y|
       v   | PLCs  |  | PLCs |--+      Device-controllers
       ^   +-+-+-+-+  +-+-+--+  |       (L1)
       :     |        |         |
       :   +--+    +--+    +--+ |
       v   |  |    |  |    |  | +   Field level devices
           +--+    +--+    +--+     (L0)
~~~~~
{: #indusarch title="Hierarchy of Functions Industrial Control Networks"}


# Challenges and Limitations

It is also evident from the ICA-95 model that the business applications are centralized in the enterprise networks where as the current trends are adopting virtualization technologies all across the systems.

## Virtualization of Components in Industrial Systems

Virtualization enables separation of software  from the hardware. It is foundation for desegregating different system components such as operating systems, management tools, service logic, and data. This allows flexible placement of  different functions in the system and on-demand scaling of resources.

In  case of Industrial control systems, by virtualizing SCADA, MES and HMI etc. {{VPLC_CONV}} the software can run on commodity hardware or general-purpose CPUs. There are several benefits to this approach - it is cost-effective since specialized hardware is not required, more agile since software upgrades can be carried out more frequently. Most importantly, a virtualized software can be placed anywhere, often close to the source of data it needs to process, thus creating a opportunities for distributed architecture.

This in turn leads to leveraging edge compute networking for multi-site integration.

While applications and services are beginning to get  disaggregated, the virtualization of PLCs themselves is  at a very early stage. Conceptually, a virtual PLC means that the controller functions are separated from the I/O modules of the devices.

## Scalability in Industry Control Networks

In the industrial control system, infrastructure is tightly   coupled   to   the   physical   environment, having   large   numbers   of   nodes   connected   through different network segments, integrated with diverse software technologies and   running   on  heterogeneous hardware platforms. This gets more complex every time new sensors or actuators are added on the factory floors.
When a new set of devices (sensors, controllers, etc.) are to be added, a general rule of thumb is to achieve this in a non-disruptive manner. As a result, a new network is created by adding new intermediate gateways for translations, switches or routers, without any coordination. This naturally leads to overheads in device management and fragility in applications, since  they need different set of interfaces, addresses, access control policies to access each network.

##  Protocol Diversity
The devices on factory floors (e.g. fieldbus devices) are controlled by PLCs often communication over a one or more  non-internet protocols such as Modbus, Profibus, CANbus, Profinet, etc {{SURV}}. There are more than 100 different protocols each with it's own packet format and are used  in the industry. When there is need to inter-connect two or more cells, corresponding translation of protocols need to be done from source and destination end points (device to controllers). Since the number of devices supported per fieldbus controller are limited (ranging from 32 to 256), the number of PLCs continue to grow as new sensor/actuators are deployed. Moreover, additional deployments are not integrated with existing network and a new network is created.

## Communication between Enterprise and Factory

There is another aspect of protocol conversion which is indirect. Instead of end-to-end connection, factory floor PDUs are transmitted as transport encapsulations in IP. This necessitates the need for firewalls to look beyond the IP header. Thus the overall manageability of networks is also complex, it is far more difficult to change device configuration than changing the traffic flowing through those devices.

Enabling virtualization capabilities requires enhancement to existing could overcome these challenges. a converged industry architecture is required to overcome these challenges. The converged technology, seamlessly integrates the industrial and enterprise protocols.


ISA-95 is poor match for automation as it lacks flexibility in integrating business services and process control. Yet any new proposal must preserve the characteristics of each zone. For example, manufacturing requires low-latency time bound operations; this includes PLCs.

# Converged Architectural Concepts

The following sections describe the foundational concepts of converged industry network architecture. It has two important design principles (A) Ability to virtualize infrastructure end-points, (B) Disaggregated I/O Modules, (C) Converged Industry Fabric.

## Overview

{{convarch}} represents a converged network fabric (bottom-left) that enables transfer of data between software system components (top-left) and the physical devices (bottom-right). The fabric is a common network infrastructure that enables all the characteristics required in the Industry control networks, such as deterministic, low-latency and real-time communications.  In {{convarch}}, "B. factory site" represents one more cells (locations) of the physical devices. Each cell group belongs to one physical site but there could be multiple sites and a cell group associated with a site. "A. Software components" emulate different OT and IT functions hosted in a cloud like environment which is distributed, i.e.  components may be located at different sites or at the edge in case to support low-latency, deterministic applications. Both field components and software components are connected over a converged network (shown as "C. <network"> in {{convarch}}), which presents a unified view of the network with characteristics for both software and field components.

## Component Virtualization

In the existing deployments, components such as HMI, Historian, MES, SCADA systems used to run on dedicated hardware. By virtualizing these systems, they can be consolidated on a single general-purpose hardware platform, which reduces the number of hardware devices and improves security of data exchanges among these systems.

Virtual PLC is a concept in which control part of factory devices is decoupled from the I/O component. With vPLCs, the I/O stays local to the machines, sensors, actuators and drives and the controller logic is a software service implemented over RT-hypervisors. By virtualizing PLC, other components can directly interface with process control to make modifications and send commands. With the support of a deterministic network fabric, now all the software components are part of the execution environment on one side of the fabric completely capable of leveraging mature IP based technologies.

Although, an exploratory work {{VPLC_CONV}} and {{VPLC_IIC}} propose I/O field-buses to be replaced with the high-speed deterministic media (such as Ethernet), the legacy systems will continue to exist for the foreseeable future. Thus, the architecture must support the communication with field-bus I/O even when the PLCs are virtualized. This implies, the use of protocol translation gateways will still be needed on cell sites.

### Edge Compute and Processing

Component virtualization enables co-location of different service functions on the same hypervisor or entirely at a different location regardless of what security zone they belong to. The constraints aware path chain can be set using {{!RFC7665}}. Moreover, it provides multiple service function chain to support different applications. This type of architecture along with NFV {{ETSI_GS_NFV_003}} can be extremely resource efficient.

Several sensors emit time-series style data, that can add to the bandwidth consumption to the information going to the cloud. Deploying big-date application closer on the edge and scale them on-demand provides a sophisticated tool to disaggregate  processing of sensory data and summarize for the cloud-enterprise applications.


### Realtime Behavior

that provides an integrated representation of PLC functions for different type of devices. closed interaction with applications to interact with I/O devices to selected traffic;
   rather, it describes a method for deploying SFs in a way that enables
   dynamic ordering and topological independence of those SFs as well as
   the exchange of metadata between participating entities.




CIN: Converged Industry Node,
CIIR: Industry-Intermediate-Router, CIBR:- Border-Router

~~~~ drawing
   .................................................................
  .             A. <software components>                           .
   .        +----------------------+                               .
   .        |  Application Nodes   |                               .
   .      +-+--------------------+ |                               .
   .      |   SCADA/MES Nodes    | |                               .
   .    +-+--------------------+ | |                               .
   .    |  virtual PLCs        | | |                               .
   .    |    +-+ +-+  +-+ +-+  | | |                               .
   .    |    |N| |2|  |1| |0|  | | |                               .
   .    |    +-+ +-+  +-+ +-+  | | |                               .
   .    |   +----------------+ | | |                               .
   .    |   |  O/S Layer     | | | |                               .
   .    |   +----------------+ | | |         B.  <factory site>    .
   .    |   |  |RT hyperV    | | - +      +----------------------+ .
   .    |   +----|-|--|------+ |-+        |  Cell   Group N      | .
   .    +--------|-|--|--------+        +-+--------------------+ | .
   .             | |  |                 |   Cell   Group 2     | | .
   .             | |  |               +-+--------------------+ | | .
   .             v v  v               |   Cell Group 1       | | | .
   .     +----------------------+     | | Fieldbus Devices|  | | | .
   .     | CIB-Router    1      |<-x->| +(@)-(@)-(@)-(@)--+  | | | .
   .    +-+--------v--|-------+ |     |   |   |   |   |      | | | .
   .    | CII- Router   X     | |     | +----------------+   | |-+ .
   .  +-+-------------v-----+ |<--yy->| | I/O Modules    |   | |   .
   .  | CII-Router      1   | | |     | +----------------+   |-+   .
   .  | +-----------------+ |<---zz-->|                      |     .
   .  | |C o n v e r g e d| | |_+     + ---------------------+     .
   .  | |  F a b r i c    | |_+                                    .
   .  | +-----------------+ |                                      .
   .  +---------------------+                                      .
   .      C. <network>                                            .
   .................................................................
~~~~~
{: #convarch title="Converged Industrial Network Architecture"}

## I/O Modules and Field Components

A manufacturing facility can be located at more than one site and each site is further divided into cells. Further the machinery, actuators, sensors are associated with the cell connected to the PLCs. These controllers run different protocols such as Ethernet, RT-Ethernet, Modbus, ProfiNet etc.

In a vPLC supported environment, the I/O cards are responsible for media access conversion from in and out of the converged fabric. Even the support for legacy PLCs is similar to vPLCs, with the role reduced to only translation function.

## Converged Fabric

Converged fabric shown as "B." in {{convarch}} is central to the architecture. The connectivity is largely Ethernet based (except I/O device interfaces), potentially running IP protocols on the switches and routers in the network.

Since this is a logical fabric, the connectivity is local on a factory floor and can be extended to multiple sites. Interconnecting different different sites will use WAN  functions. The fabric breaks the hierarchical structure and topology can now be designed as fat-tree (or leaf-spine) network which provides overall more number and multiple deterministic paths between two end points.

A key characteristic of legacy Industry networks is that they do not require frequent changes and therefore, topology changes are not dynamic. The fabric could potentially use a combination of software-defined connectivity with IP routing protocols. The routing protocols will maintain the infrastructure reachability among the network nodes and software-defined solutions will manage flow of traffic in a deterministic manner addressing the low-latency and deterministic data delivery of certain type of flows.


# Requirements

## General Requirements

  A converged industrial network spans between the applications in the cloud to the devices on factory floor. It is responsible for moving traffic securely between these 2 end-points in a cloud-oriented manner.
        1. Performance and Deterministic Behavior Shorter addresses are inherent to industry control systems to provide implicit determinism. For this purpose, the industrial networks use fieldbus interface with the controllers.
        2. reserving Safety and Task outcomes
        3. Interoperability with IP-world machines

To develop further on different type of address format support. From smaller address of legacy devices to IT based applications with IP address.


## Legacy device support

:
: Support for protocol formats and their core capabilities.
:
: Support for traffic profiles for different types of services
:
: Support for security and separation as designed in OT systems.

## Requirements from Emerging Trends

  1. Unified addressing Support device to cloud communication (remote operations)
  1. Virtualization (virtual PLCs, digital twins)
  2. High-volume data emission (analytics and surveillance)
  3. Explicit location awareness (to determine edge networks, latency sensitive controls, safety operations).
  4. Enhanced Industry data and device security (movement of sensitive data and remote control)

## Device Functions
These functions apply to end nodes as well as network nodes or other gateways in the network.

The topologies in the manufacturing zones do not change very frequently and devices are also designed for long-term use with minimal time between the failures. Such design considerations may be used to simply network operations and configurations.

Assuming this is a layer 3 network architecture, there should be  an assignment and association between the network address and end devices' physical addresses. Note that legacy devices are either on serial bus or their information is carried over Ethernet media.

Further motivation and analysis for adapting to OT/IT asymmetric address formats is covered in {{?I-D.draft-km-industrial-internet-requirements}}.

Additionally, adapting these devices to network layer requires support for the following mechanisms:

### Device Specific functions

- discovery and on-boarding
- Device identification and authentication
- Device addresses and their assignment and management

### Transmission (Transport) Mechanisms
Currently, L0 and L1 devices do not use any transport protocol. The data is embedded after control header. With a network layer solution, TCP maybe too heavy for field-bus devices. Some other means of assuring device delivery will be needed.

### Routing considerations to provide safety & security
Routing protocols will be necessary as the scale of the devices grow at the same time it should be kept simple.
Possibly, Interior Gateway Protocol (IGP) will be deployed. Here it may be useful to provide guidelines on IGP features that provide distribution of routes (for different devices), path information.

### Traffic Profiles for different type of data
Differentiating traffic and assigning priorities is required so that important data is not dropped. This is in addition to use of Detnet for time-sensitive services.

Different type of data can include - process data (high priority), monitoring data (low priority), fault, alarms, signals data (high), health-check sensors data (medium), etc.


# IANA Considerations

This document requires no actions from IANA.

# Security Considerations

This document introduces no new security issues.

# Acknowledgements

--- back

# Appendix A.  Purdue Model (ICA-95) {#Appendix}

The International Society of Automation (ICA) has developed a model {{ISA95}}  to describe automated
interfaces between enterprise and control systems.  In this widely deployed hierarchical model, five levels are defined and they follow a strict ordering of interfaces across the  levels. At the lowest level  0, are the physical devices while enterprise applications are at level 5. In between these two levels, there are several supervisory, management, and intermediate data collection applications that provide information to

~~~~ drawing
  |      +-------------------------------+  Enterprise
  | L5   |    Enterprise applications    |  Security
  +--    +-------------------------------+  Zone
  |      +-------------------------------+
  | L4   | Gateways, servers (ops, mgmt) |  IDMZ
  +--    +-------------------------------+
  |      +-------------------------------+
  | L3   |    Supervisory controls       |  Industry
  |      +-------------------------------+  Security
  | L1   |  Device control               |  Zone
  |      +-------------------------------+
  | L0   |Sensors, Actuators, Robots, etc| (cells or zones)
  +--    +-------------------------------+
~~~~
{: #Automation title="ISA 95 or Purdue model of Automation Pyramid"}

## Separation between Manufacturing and Enterprise Networks
The ICA-95  architecture recommends hierarchy, thereby a separation between factory devices and applications through three different security zones called Manufacturing, DMZ and enterprise zones as shown in {{Automation}}  as below:

- Enterprise Security Zone:
: The IT applications reside in enterprise networks and perform tasks necessary for business operations such as inventory control, supply-chain logistics, schedule and capacity planning. They need to collect data from the OT systems in order to make those decisions.

- Industrial Demilitarized Zone:
: The OT and IT networks were designed to prevent direct communication between them. The IDMZ serves as an information sharing layer between the IT and OT (L4 and L3) systems. This indicates that additional security rules, inspection and protection of device identity and access is necessary when transiting from L3 to L4.

- Manufacturing Zone:
: Consists of Levels 0 through 3 site wide production system.  Operations at level 3 (L3) Support site-wide view of the production system. They also provide data to L4. Area supervisory control (L2) performs operation and control over a zone or smaller area in a production floor. Each area has specific set of tasks or operations to perform. Basic control  at level 1 (L1) is for the actual control of the equipment. The L1 components such include PLCs; they send commands to L0 equipments to perform tasks (e.g. start motor, alter pressure level, or reduce motor speed). Finally, actual process takes place at level 0 (L0). At this level for the process equipments performing actual operations are performed. This include equipment and devices such as motors, pressure valves, temperature, speed, etc sensors, etc.

The devices or controllers at level 1 are the ones of specific interest for virtualization and the corresponding challenges are covered in later section.

## Collaborating with SDOs with Industry Network Focus

The paradigms of networking in OT are quite different than IP based best-effort networking protocols. Yet, IETF protocols are extensively used in OT applications. Often, it is not possible to get contributors directly from the OT sectors, then it would make more sense to coordinate with well-established consortia where OT scenarios and requirements are is discussed may be utilized. Two well established foundations are IIC {{IIC}} and OPC-UA {{OPC}}.
For example, a {{IIC_TALK}} provided overview of IIC activities.

Industrial IoT Consortium (IIC) provides use cases, scenarios, and best-practice frameworks to solve specific problems and solution pain points. It is a rich resources of case studies and demonstrations of different test beds. The IIC itself is not involved in standards development, but may help in formalizing requirements, further insights into solutions developed in IETF, and potentially help adoption of those solutions.

Open Platform Communications-Unified Architecture (OPC-UA) provides interoperability across different hardware platforms using a standard data model. It standardizes various information models, corresponding client-server architecture and defines necessary access mechanisms to those information models.
The OPC-UA is an abstraction layer to provide common interface to different data look-up and event notifications. A number of information models are provided by OPC-UA can be found here {{OPC_INFO}}.
Foe example, OPC has a specification on PLCs. It abstracts PLC specific protocols (such as Modbus, Profibus, etc.) into a standardized interface allowing HMI/SCADA systems to interface with a middleware that converts generic-OPC read/write requests into device-specific requests and vice-versa.

> Note: OPC-UA information model similar to YANG?

IETF solutions will focus on leveraging or extending IETF technologies for IT and OT integration which is at the infrastructure or communication layer. Thus, providing protocols that could potentially benefit higher-level OPC-UA work.

Both IIC and OPC could provide guidance to the lower level work.

- For Discussion: assuming there is an IIN framework - how does it fit in the OPC-UA architecture and facilitate adoption of existing information models.


