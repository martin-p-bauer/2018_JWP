# Example Use Case [Laura Daniele]
Describe an example use case that instantiates the problem space, is as simple as possible, but shows the advantages of semantics and can be used in the following subsections.

Smart Home and Energy Efficiency Domain
Demand Response: Users can offer flexibility to the Smart Grid to manage their smart home devices by means of a Customer Energy Manager (CEM). The CEM is a logical function for optimizing energy consumption and/or production that can reside either in the home gateway or in the cloud. The interoperability of a device with other devices and with the CEM should be guaranteed regardless of their brand/manufacturer, because the user wants to be able to buy any washing machine they want and still have it communicate with the other devices that are already in their home. Some examples scenarios include the scheduling of appliances in certain modes and preferred times using power profiles to optimize energy efficiency and accommodate the user's preferences. For example, the user might want the washing done by 5:00 p.m. with least electrical power costs, or prefer to limit their own energy consumption up to a defined limit.

Collection and analysis of meter data: The collected meter data is provided by smart meters through two different interfaces on the meter. One (upstream) interface is used by the meter/grid operator for billing and grid management. This data is fed into the Head End system. Another interface provides real-time data for energy management. This data is fed into a Home Energy Gateway. Historic meter data can be retrieved from the Head-End system. Real-time data is retrieved from the Energy Gateway. Data Analytics applications analyse (real-time) consumer data to give insight in consumer behaviour and recommendations for energy efficiency.

The demonstrator produced during the recent DSF study for interoperability for the European Commission (SMART 2016/0082) in close collaboration with industrial stakeholders and appliance manufactures implements an energy gateway that uses SAREF and SAREF4ENER as overarching ontologies to combine data represented by oneM2M resources on the smart grid side (based on e.g., the IEC 61970 CIM standard), with data represented by SPINE resources on the Smart Home side (based on the CENELEC EN 50631-1 standard), and data represented by COSEM objects/ OBIS codes on the smart meter side (based on the IEC/CENELEC 62056 COSEM standard). 

Let us consider now the additional case where the habitant of the house is an elderly that needs support at home, as well as to be continuously monitored (i.e. wellbeing for aging well). In order to implement such use case:
  1.	the habitant/elderly needs to be provided with a smart BAN (Body Area Network) for the monitoring and control of its vital    signs, status and activities. This smart BAN mainly comprises, in respect of its habitant/elderly embedded device part (smart BAN Cluster), medical/wellbeing sensors, wearables, a BAN coordinator or hub (e.g. a smart-phone, a smart-watch) with in particular data concentrator and network gateway roles. The data concentrator is used for data collection and has also to be provided with embedded data analytics functionalities for local alarm management, local monitoring/control and habitant/elderly assistance purposes. The network Gateway is mainly used for data sending to the remote monitoring/control servers and applications located within caregivers or relatives premises. Let us note that, for security/safety reasons, actuations on habitant/elderly BAN devices have not been actually considered. 
  2.	this smart BAN has to interact with the Smart Home and some of its appliances mainly for the following purposes: habitant/elderly positioning inside the house (e.g. through beacons on the walls), habitant/elderly activity tracking, verification of interactions with key appliances (e.g. with a scale for weight measurement, or for verifying if fridge or cooker was used, or if a medication box was opened), habitant/elderly comfort management (e.g. maintaining a given temperature/humidity/luminosity level in accordance with habitant/elderly condition requirements, as well as with energy efficiency objectives that could be already parameterized for the Smart Home).

The additional use case (i.e. elderly at home monitoring and support) high level architecture is depicted in Figure 1.

![](img/SemInteropElderlyHomeUseCase.png)

In a such environment and use case, it is first mandatory to address security and privacy by design since we are dealing with eHealth and personal safety highly critical data and applications (even if actuations within BANs are not yet considered for quite all the existing use cases). It is also mandatory to address interoperability, in particular since:
1.	At least heterogeneity of medical devices and measures has to be masked at application level,
2.	At the operational level and from the hospital management information system (MIS) point of view, a new patient’ BAN integration into existing monitoring and control systems has to be carried out as far as possible without any redesign of those systems, even partially,
3.	At smart BAN level and from the end user perspective, any new sensor integration has to be transparent for the elderly, with a minimum number of easy operations.

For addressing all the aforementioned requirements, interoperability will have thus to be handled at multiple levels for our elderly at home additional use case:
•	Device level for in particular handling point 3 and to some extend point 2,
•	Informational level, i.e. data and semantic, for in particular
    o	handling point 1, point 2, point 3, 
    o	data/information sharing across systems, i.e. Smart BAN and Smart Home systems,
    o	enabling semantic-based embedded data analytics. This will be used here for alarm management, monitoring/control and habitant/elderly/caregivers assistance purposes,
    o	for facilitating cross-domain interactions, in particular between healthcare, wearables and Smart Home.
•	Network level for mainly handling point 2 and intra/inter systems interoperability.
