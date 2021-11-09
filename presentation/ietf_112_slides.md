---
type: slide
slideOptions:
  transition: slide
  theme: white
---
# Framework For Integrated Industrial Networks
 draft-iotops-km-iiot-frwk-00

Kiran Makhijani
Lijun Dong 
(Futurewei)

             

---

## Motivation
To what extent, how and where IETF technologies can be leveraged for IIoT?
- **Better OT/IT integration**: all the way  from application to device
- **IIoT Cloudification**: Extension of OT networks to the edge or cloud

- **Virtualization**:  of software PLCs
    - a growing number of components (SCADA, MES, HMI, etc.) are becoming cloud based.
    - Device instances interact with different applications


----

### What's in the Framework

 1. Integrated Industry Network (IIN)
    - design and technical requirements 
        - From device side as well as networks nodes
 2. Infrastructure (limited-domains model)
    - Interconnection between public and special purpose networks using LDN nomenclature (RFC 8799).
    - Remain aligned with Industry control architures
 3. Stakeholders
    - Identified 3 bodies of SDOs to approach to
---

## ISA-95  (Security Zones) Purdue Model
![](https://notes.ietf.org/uploads/upload_8962979bc07832a5d02b0a9cc62d3623.svg)
>Note: pay attention to zones: Enterprise, IDMZ, Industry security zones.

----

### Security Zones or Boundaries between IT/OT
  *  <div style="color: #29f;">Enterprise Security Zone:</div> Typical IT applications 
      * perform tasks necessary for business operations such as inventory control, supply-chain logistics, schedule and capacity planning.
  * <div style="color: #29f;">Industrial Demilitarized Zone:</div> An information sharing layer since  OT and IT networks were designed to prevent direct communication between them.  
      * Translation of security rules, inspection and protection of device identity and access is necessary when transiting from L3 to L4.
   *  <div style="color: #29f;">Manufacturing Zone:</div> Levels 0 through 3 site wide production system.

----

###  Distributed Architecture (Level Placements)
##### In a cloud-based architecture, levels may be distributed to edge compute networks, emulates LDN.
 ![](https://notes.ietf.org/uploads/upload_ff0cec1ab7ce1ee5d841fd9a263d7359.png)

---


## Limited Domain Networks
Device Perspective
<todo></todo>

---


## Requirements

* Device Perspective
    * device discovery?
* Network Interactions
    * tunnel free, efficient methods
    * 


---


## Stakeholders

* IIC: Will provide a lot of opprtunities for coordination.
    * rich resource of use cases and organizations involved in OT development.
* OPC-UA: provide an abstraction of data. 
    * could certainly benefit from communication technologies.
*  IEC/IEEE 60802 project: Partnership between OT and IT. 
    *  seem to be working on different profiles related to OT scenarios.
    *  close coordination with OPC-UA

---


## Fragment Styles



---


## Print your Slides

Down below you can find a print icon<i class="fa fa-fw fa-print"></i>.

After you click on it, use the print function of your browser (either CTRL+P or cmd+P) to print the slides as PDF. [See official reveal.js instructions for details](https://github.com/hakimel/reveal.js#instructions-1)

---

# The End
