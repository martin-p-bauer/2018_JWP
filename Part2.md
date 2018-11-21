# Part 2

## Introduction [Martin Bauer]
Semantic technologies have recently gained significant support in a number of communities, in particular the IoT community. An important problem to be solved is that on the one hand it is clear that the value of IoT increases significantly with the availability of information from a wide variety of domains, on the other hand existing solutions target specific applications or application domains and there is no easy way of sharing information between the resulting silos. Thus a solution is needed to achieve interoperability between the silos. As there is a huge heterogeneity regarding IoT technologies on the lower levels, the semantic level is seen as a promising approach for achieving interoperability, i.e. semantic interoperability.
As a basis for this, semantic technologies have reached a good level of maturity and a number of standards and de-facto standards are available to implement semantic-based solutions. 
However, currently the widespread use is hindered by the fact that developers and system architects are not familiar with semantic technologies. The respective knowledge is still primarily limited to a group of experts. Thus, the purpose of this Whitepaper is to spread this knowledge further and in particular to show the developer community how semantic solutions can be implemented and how semantic interoperability can be achieved. The goal is to show the practical feasibility of the approach.
The approach of the paper is to take a small, but relevant example, and go through different aspects and activities that are needed when developing semantic solutions. For each of the steps relevant types of useful tools are explained with references to an appendix that provides a list of actual tools with short descriptions and relevant links, so, depending on the respective requirements, an appropriate tool can be chosen.

## Problem Description [Michelle Wetterwald, Marc Girod-Genet]

In this section, we describe the problem space in which semantics can be applied, in particular we explain why it is needed to provide platform, system or domain interoperability.

Several studies have demonstrated the fragmentation of the IoT eco-system in terms of standardization, available technologies and M2M service platforms. Accordingly, measurements and data available in one system or implementation are often not accessible by a different system. Furthermore, these systems and the data they handle are often still strongly dependent of the vertical domain in which they are implemented. 

Interoperability has been considered at various levels: technical (connectivity, network, syntactic), informational (semantic or business context) or even organizational. Technical levels cannot be easily achieved when addressing integrated platforms. The semantic or data level is thus the next level where interoperability can be envisioned. Furthermore, the different systems must share the same vocabulary and understand in an identical manner the information they exchange, while facilitating the design of service compositions. 

There is a need for a common model that describes a system and its components and can be understood by different implementations and platforms. It should provide a formalized specification of that system, including its main concepts, the relationship between its main components and their attributes. It should indicate the meaning of the data shared by a device, which can be understood by machines from different origins. Semantic interoperability enables interoperability at data level between platforms and IoT systems, but also between verticals domains. When an ontology is defined for one device from a vertical domain, e.g. agriculture, a generic interworking is made possible, i.e. the data it shares can be understood by machines and devices operating in other domains, for example smart mobility or smart city. It enables the IoT applications to make smarter decisions because they are able to collect, understand the meaning and process data from all sorts of devices. In that context, there is no further need to develop one-to-one interfaces and less risk to make errors when using external data.

Semantics and ontology definition can bring a valuable solution, as it defines a common and abstracted sub-layer above the services and platforms definition. Semantics interoperability thus enable the sharing of data across systems, avoiding the definition of a new common data model every time two different systems need to exchange information or the costly misinterpretation of data received from an external system.

As already aforementioned, one of the first interoperability level to take care of is at informational level, i.e. at data and semantic level. It is mandatory to address since it allows data heterogeneity management, both within a single platform and even across platforms (provided that the data model becomes a unified / standardized one). One good example of that is the Bluetooth LE GATT (Low Energy Generic Attributes) profile that has been standardized by the Bluetooth Special Interest Group (SIG) and enables interoperability of Bluetooth devices [https://www.bluetooth.com/specifications/gatt].

![](img/RoomExample.png)

Figure 1: Simple example of a house room

Let us now take the simple problem of a house room with a black box on a wall (see figure 1), e.g. a sensor that is providing the following instant value: 22°. A visitor of the house has as much power of reasoning as humans do and is therefore guessing (due to the position of the black box, the value provided on the black Box screen  ̶  22°  ̶ , his central European location) that the provided value is a temperature expressed in degree Celsius. A machine (e.g. a Device, an automated process, an application…) for its part is not able to do a lot with this instant value (22°) since it does not know how to analyze this raw data, mainly:

•	the meaning of the data, called metadata, e.g. in our home example a temperature measurement, with “Temperature” as name, ‘t’ as acronym, “°C” as unit of measure, “float” as measurement domain and 22 as value. With this metadata knowledge, few simple data analytics can already be performed, like e.g. in our home example, verifying if a  Temperature ‘t’ is not higher than 26,

•	and the context of the data, extending the metadata and called ontology, like e.g. in our home example, the information of the sensor that provides the data, the associated positioning and geo-localization, environment, room and home ID, home owner information. With that extended semantic knowledge, more powerful semantic data analytics can now be performed, like e.g. in our home example, which are the collocated houses that have the same Temperature value. 

Ontology design (i.e. specification, formalization) and implementation are thus mandatory for data heterogeneity management and semantic interoperability. It facilitates data/information sharing across systems and enables semantic-based embedded data analytics (e.g. for automated alarm management or control operations). If the ontology incorporates common upper level semantics, like e.g. service definition, then it enables data sharing at application level and also facilitates cross-domain use cases handling.

The specification of a semantic data model corresponds to the definition of concepts that characterize the data and its environment, associated with the links between those concepts. This is generally materialized through a diagram/graph where the concepts correspond to classes or tree nodes, and relations correspond to tree edges labelled by the relation type. For the simple example depicted in Figure 1, the black box on the wall is e.g. a device (this is a first concept) that makes a measurement (this is a second concept, linked to the first one by the relation ‘makes’). Concerning the formalization of the data model, this corresponds to the transcription of its corresponding concepts and their relations within a formalized description language. This computing description language insures in particular that the data model is readable and interpretable by both machines (e.g. Devices, automated processes, applications…) and humans in a unique and unambiguous way.

Next sections show, using a specific use case, how semantic interoperability can be implemented and deployed.

## Example Use Case [Laura Daniele, Marc Girod-Genet, Martin Bauer]
*Describe an example use case that instantiates the problem space, is as simple as possible, but shows the advantages of semantics and can be used in the following subsections.*

In this use case a smart home with smart devices is to be connected to the smart grid. The smart home resident wants to optimize the energy consumption of the house, but still be in control of key aspects, e.g. when the washing has to be done, when the batteries of the electronic vehicle have to be recharged, and that the temperature in the house is kept within a certain range etc. The smart grid company offers the smart home resident a special tariff with significant discounts during times when a surplus of energy is available in exchange for some control on the energy consumption. Thus the smart grid company gets means to balance the overall energy consumption and the smart home resident lowers the energy bill without a significant loss of convenience.

In order to implement the scenario, different systems have to be integrated allowing the following:
 * connect controllable user devices in the smart home
 * connect the smart grid with the smart home
 * provide the smart home resident with means to define operation policies for the devices
 * provide the smart grid operator with means to define time-dependent energy costs and request an energy-consumption profile
 * optimize energy consumption based on the time-dependent energy costs and the energy-consumption profiles in line with the operation policies and a possible consumption limit

To achieve interoperability between the systems, agreement on the interfaces and the modelling of information is necessary. In this paper we will show how the relevant information can be modelled on a semantic level to achieve semantic interoperability. 

Examples of what needs to be modelled:
 * Device 
   * status
   * control
   * monitoring
   * energy consumption profile
   * operation policy
 * Estimated energy cost timeline
 * Energy consumption limit

Customers can offer flexibility to the Smart Grid to manage their smart home devices by means of a Customer Energy Manager (CEM), a logical component that controls and optimizes the energy consumption in a smart home. The CEM is a logical function for optimizing energy consumption and/or production that can reside either in the home gateway or in the cloud. The component that collects and analyzes energy consumption is a smart meter. Example use cases that require interoperability and involve devices in the smart home, the CEM, smart meters and the smart grid are the following:
- configuration of devices that want to connect to each other in the home network, for example, to register a new dishwasher to the list of devices managed by the CEM;
- (re-)scheduling of appliances in certain modes and preferred times using power profiles to optimize energy efficiency and accommodate the customer's preferences;
- monitoring and control of the start and status of the appliances; 
- reaction to special requests from the Smart Grid, e.g. incentives to consume more or less depending on current energy availability, or emergency situations that require temporary reduction of power consumption. 

These use cases are associated with the user stories described in IEC TR 62746-2 [i.6], which include, among others, the following examples:
•	User wants to do basic settings of his/her devices.
•	User wants to know when the washing machine has finished working.
•	User wants their washing done by 5:00 p.m. with the lowest electrical power cost.
•	User likes to limit his own energy consumption up to a defined limit.
•	User allows the CEM to reduce the energy consumption of the freezer in a defined range for a specific time, if the grid recognizes (severe) stability issues.
•	Grid related emergency situations (e.g. blackout prevention).

Let us now consider the additional case where the resident of the house is an elderly that needs support at home, as well as to be continuously monitored (i.e. wellbeing for aging well). In order to implement such use case:
  1.	the resident/elderly needs to be provided with a smart BAN (Body Area Network) for the monitoring and control of its vital    signs, status and activities. This smart BAN mainly comprises, in respect of its resident/elderly embedded device part (smart BAN Cluster), medical/wellbeing sensors, wearables, a BAN coordinator or hub (e.g. a smart-phone, a smart-watch) with in particular data concentrator and network gateway roles. The data concentrator is used for data collection and has also to be provided with embedded data analytics functionalities for local alarm management, local monitoring/control and resident/elderly assistance purposes. The network Gateway is mainly used for data sending to the remote monitoring/control servers and applications located within caregivers or relatives premises. Let us note that, for security/safety reasons, actuations on resident/elderly BAN devices have not been actually considered. 
  2.	this smart BAN has to interact with the Smart Home and some of its appliances mainly for the following purposes: resident/elderly positioning inside the house (e.g. through beacons on the walls), resident/elderly activity tracking, verification of interactions with key appliances (e.g. with a scale for weight measurement, or for verifying if fridge or cooker was used, or if a medication box was opened), resident/elderly comfort management (e.g. maintaining a given temperature/humidity/luminosity level in accordance with resident/elderly condition requirements, as well as with energy efficiency objectives that could be already parameterized for the Smart Home).

The additional use case (i.e. elderly at home monitoring and support) high level architecture is depicted in Figure 1.

![](../SemInteropElderlyHomeUseCase.png)

In a such environment and use case, it is first mandatory to address security and privacy by design since we are dealing with eHealth and personal safety highly critical data and applications (even if actuations within BANs are not yet considered for quite all the existing use cases). It is also mandatory to address interoperability, in particular since:
1.	At least heterogeneity of medical devices and measures has to be masked at application level,
2.	At the operational level and from the hospital management information system (MIS) point of view, a new patient’ BAN integration into existing monitoring and control systems has to be carried out as far as possible without any redesign of those systems, even partially,
3.	At smart BAN level and from the end user perspective, any new sensor integration has to be transparent for the elderly, with a minimum number of easy operations.

For addressing all the aforementioned requirements, interoperability will have thus to be handled at multiple levels for our elderly at home additional use case:

•	Device level for in particular handling point 3 and to some extend point 2,

•	Informational level, i.e. data and semantic, for in particular

 - handling point 1, point 2, point 3,
 - data/information sharing across systems, i.e. Smart BAN and Smart Home systems,
 - enabling semantic-based embedded data analytics. This will be used here for alarm management, monitoring/control and resident/elderly/caregivers assistance purposes,
 - for facilitating cross-domain interactions, in particular between healthcare, wearables and Smart Home.

•	Network level for mainly handling point 2 and intra/inter systems interoperability.
