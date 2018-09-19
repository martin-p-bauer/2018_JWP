# Ontology Selection / Creation [Amelie Gyrard, Iker Esnaola, Izaskun Fernandez]

Ontology Selection/Creation diagram:

![Ontology selection/creation diagram flow](https://image.ibb.co/d4iAxT/Diagram.png)

## Identify ontology requirements

First of all, it is necessary to think about the objectives of the ontology. For that purpose, filling an ORSD (Ontology Requirements Specification Document) may be helpful. It facilitates identifying why the ontology is being built, what its intended uses are, who the end users are, and which requirements the ontology should fulfill.

- ORSD guide: http://oa.upm.es/5474/1/INVE_MEM_2009_64393.pdf

#### Use case ontology requirements
This is an excerpt of the OSRD created for the use case:

![OSRD example for the use case](https://image.ibb.co/iO3gOo/OSRD_example.png)

## Reuse existing ontologies

Once the objectives of the ontology are clear, it is necessary to actually have an ontology that fulfills those objectives. Instead of creating an ontology from scratch, it is a good practice to reuse existing ontologies when possible due to the following reasons [2]:

- The sharing and reuse of ontologies increase the quality of the applications using them, as these applications become interoperable and are provided with a deeper, machine-processable and commonly agreed-upon understanding of the underlying domain of interest.
- It reduces the costs related to ontology development because it avoids the reimplementation of ontological components, which are already available on the Web and can be directly – or after some additional customization – integrated into a target ontology.
- It potentially improves the quality of the reused ontologies, as these are continuously revised and evaluated by various parties through reuse.

According to [2], ontology reuse can be understood as a three-step process: (i) ontology discovery, (ii) ontology selection, and (iii) ontology integration.

### (i) Ontology discovery 

It consists in finding appropriate ontologies that meet our requirements. This task can nowadays be facilitated due to the numerous ontology catalogs to find existing ontologies. Some of them, extensive analysis of ontology catalogs for smart cities can be found in [9]:
 
- Linked Open Vocabularies for Internet of Things (LOV4IoT) references more than 440 ontology-based projects relevant for IoT. It covers more than 20 domains: IoT, Wireless Sensor Networks (WSNs), Web of Things (WoT), smart home, smart energy, healthcare, smart city, robotics, etc. LOV4IoT is highly maintained and references more and more ontology-based projects and new domains are covered.
   
- OpenSensingCity, an ontology catalog for smart cities. This catalog might be not maintained anymore after the end of the project (ANR french project).
  
- Ready4SmartCities, an ontology catalog for smart cities. It seems it is not maintained anymore. 

- Linked Open Vocabularies (LOV) designed by the Semantic Web community. This catalog is highly maintained and references ontology fitting their best practices criteria (e.g., ontology metadata).

TO DO?:
We can reuse well-written paragraphs about ontology catalogs from this paper (third revision ongoing) if needed: Building IoT based applications for Smart Cities: How can ontology catalogs help? [Gyrard et al. IEEE IoT Journal 2017] (Impact Factor 7.5)

#### Use case ontology discovery

Since the use case presented in this report is more oriented to smart homes rather than smart cities, two of the aforementioned repositories (namely OpenSensingCity and Ready4SmartCities) have been dismissed for this task.

In the following Figure, a screenshot of LOV4IoT is shown. With regards to the “Smart Home, Smart office, Building Automation, Activities of Daily Living Catalog” to which the presented use case belongs to, SAREF is one of the top recommended ontology: shared online, referenced by the LOV community since it follows a set of best practices requested by the community, and highly maintained.


![LOV4IoT screenshot](https://image.ibb.co/g7Gzb8/lov4iot.png)

As for the LOV, the following Figure shows ontologies related to the term “electric consumption” which is relevant for the use case at hand as it has been shown in the OSRD.

![LOV screenshot](https://github.com/martin-p-bauer/2018_JWP/blob/master/img/lovExample.png)


### (ii) Selection of suitable (parts of) ontologies

This task deals with assessing the usability of an ontology with respect to the use case requirements. This may end up being an arduous task due to the different criteria that may make ontologies suitable for a certain use case [3]. These criteria encompass the content of the ontology and the organization of their contents, the language in which is implemented, the methodology that has been followed to develop it, the software tools used to build and edit the ontology, and the costs that the ontology will be necessary in a certain project Furthermore, the scarce documentation of ontologies may difficult even more this process.

In order to ease this selection phase, we recommend to look first at ontologies supported by standardization activities (e.g., W3C SOSA, SAREF, W3C WoT, oneM2M, SmartBAN, etc.).

In case the developer needs to reuse only a subset of classes and properties of the ontology, instead of the whole ontology, an extractor tool (see Appendix section) can be used.

Limitations: Indeed, we would need some ontology ranking algorithms to help better developers find suitable ontologies for their needs.

As an illustration, in the context of our room and temperature sensor simple example already introduced in Figure 1 (see problem description section), we are in a Smart Home application domain. In such vertical, the reference ontology that meets the use case description is SAREF. Therefore, by using SAREF ontology, our temperature sensor can be viewed as a Device (saref:Device):
•	With saref:Sensor as device category,
•	That is provided with e.g. a Description (String), a Manufacturer (String), a model (String), a State (e.g. on or off) as properties,
•	That offers/performs sensing expressed as saref:Function, with saref:SensingFunction (which has a range, a sensing time and the sensor type  ̶  ‘Temperature’ in our example  ̶  as properties) as category, saref:GetCommand as command (i.e. GetTemperature in our example), 
•	and that is used for sensing a temperature of type saref:Temperature. This ‘Temperature’ property (a saref:Property) has a unit of measure of the type saref:UnitOfMeasure (°C in our example), and has a Value (22 in our example).
This can finally be modeled through the UML diagram presented in Figure below.
![](../img/RoomExample_SAREF.jpg)


#### Use case ontology selection
After having identified the ontologies that may be suitable for the use case at hand, it has to be decided which ontologies to reuse as they are. For the use case at hand, the reuse of SAREF as it is may be a good decision, due to its support by a standardization body. However, SAREF does not cover all the use case requirements, so other ontologies need to be reused.

If ontologies covering the same domains are imported altogether, they may overlap to a greater or lesser extent in some of their parts. Therefore, in these cases parts of ontologies can be reused to avoid redundancy issues and enhance interoperability. The m3-lite ontology contains covers terms related to “properties” that are not exhaustively captured in SAREF. However, the coverage of the m3-lite is wider than needed, so we only need the subclasses of qu:QuantityKind. For that purpose, the Module Extractor Tool (see Appendix).

![M3-lite screenshot](https://github.com/martin-p-bauer/2018_JWP/blob/master/img/QuantitiyKindExample.png)

After executing it, we get an ontology module named “m3-lite_QuantityKindModule” that contains all the subclasses of class qu:QuantityKind plus the other necessary axioms for the given concepts. Comparing this module with the original m3-lite ontology, we can see how the size has been reduced, including only the terms that are related to our use case (in this case, the properties). The number of axioms have been reduced from 2035 to 360, and the number of classes from 451 to 178.

![equivalence example screenshot](https://github.com/martin-p-bauer/2018_JWP/blob/master/img/equivalentExample.png)

### (iii) Ontology integration 
Finally, the selected ontology or ontologies may need to be customized in order to adapt them and satisfy the use case’s requirements. This customization may involve additional modification and integration operations such as extraction of ontology parts or even content and structural modification or extension.

When more than one ontology (or parts) are integrated, ontology matching tool can be performed to return a potential alignment between two ontologies. Some basic ontology matching tasks consist in setting relationships such as:
- Equivalences between concepts (with the owl:equivalentClass property)
- Subsumptions (with the rdfs:subClassOf or rdfs:subPropertyOf properties)
- Disjointness between entities (with the owl:DisjointOf property)
- Labels an comments to deduce similarities (with rdfs:label and rdfs:comment properties)

#### Use case ontology integration

After having both the SAREF ontology and the “m3-lite_QuantityKindModule” module, we need to integrate them. The process to be followed towards this goal will depend on the ontology design tool used. Once integrated, it needs to make explicit that the class saref:Property and qu:QuantityKind have the same adjacent semantics. That is, the equivalence between the two concepts needs to be set. This equivalence can be set with the following axiom:

saref:Property owl:equivalentClass qu:QuantityKind

Likewise, the equivalence can be set in the ontology design tool.


## Create new ontology / Extend existing ontologies

If the existing ontologies do not meet all the requirements captured in the OSRD, ontologies need to be extended and maintained. 

In case no existing ontologies have been found for our specific requirements captured in the OSRD, there might be a need to develop your own ontology. 

For a more exhaustive ontology creation guide, we advice excellent documentation and methodologies: the NeOn methodology for ontology engineering[1], and the ontology development 101 [5]).

Protégé [6] is one of the most popular software to learn how to create ontologies. Protégé provides a Graphical User Interface (GUI) to design and develop ontologies. You can either set up Protege on your computer or use the web collaborative Protege tool. We provide a set of excellent tutorials to develop your first ontology with Protégé (see Appendix Section.

When creating or extending an ontology, it is advisable to follow the modularisation principle by separating the required knowledge in well-decoupled ontology modules. The main benefits of this principle are: 1) scalability for querying data and reasoning on ontologies, 2) scalability for evolution and maintenance, 3) complexity management, 4) understandability, 5) context-awareness and personalization, and 5) reuse [4]. For example, when some of the ontology modules are updated, thanks to the modularization, the impact of these changes in other modules and the global ontology is minimized. IoT-O [7] and [8] FIESTA-IoT ontologies are good examples of ontology modules.

Note that the extension and maintenance of ontologies require proper understanding on the resulting business impact. For instance a smart appliance using an extended ontology might no longer be interoperable with another smart appliance using the initial version. A maintenance strategy might have therefore to be defined prior to the implementation of an extension.

It is also recommendable to use Ontology Design Patterns (ODP) (see Appendix Section) as building blocks to create new ontology modules. An ODP is a modeling solution to solve a recurrent ontology design problem. The ODP repository collects and makes ODPs available on the web. It may contain a solution created by somebody else who already faced the same modeling challenge.

Once the ontology is created, it is advisable to align it with related ontologies and upper-level ontologies (i.e. DUL) to make the ontology applicable to similar problems in different domains and scenarios.

TO DO? should we provide more examples protege with smart home ontology? How to create a concept, and property relevant for smart home (show protege interface, and code)?

TO DO? Check and merge with ontology development section (Part2.md)?

## Ontology Selection
Most of the time you already have some keywords and key phrases in mind to build the system or application. For the smart domain, keywords are “room temperature” “actuators”, “humidity”, those keywords can be mapped to concepts within ontologies.
Ontology catalogs can provide such browsing functionalities with specific keywords.

## Application of Ontology Selection to Use Case

*The use case needs integration and control of smart devices at home and the connection to the smart grid which happens to be supported by the standardized ontology SAREF and its smart energy extension SAREF4ENER. The selection of these ontologies - ideally as opposed to some other non-standard options - should be described in this section. The following paragraph was originally part of the use case section, but the selection of ontologies should not already be discussed there.*

*The demonstrator produced during the recent DSF study for interoperability for the European Commission (SMART 2016/0082) in close collaboration with industrial stakeholders and appliance manufactures implements an energy gateway that uses SAREF and SAREF4ENER as overarching ontologies to combine data represented by oneM2M resources on the smart grid side (based on e.g., the IEC 61970 CIM standard), with data represented by SPINE resources on the Smart Home side (based on the CENELEC EN 50631-1 standard), and data represented by COSEM objects/ OBIS codes on the smart meter side (based on the IEC/CENELEC 62056 COSEM standard).* 

Requirements and competency questions for the energy efficiency use case:
The main requirement is to establish a common terminology to be shared by devices from different manufacturers and using different protocols to express the concept of power profile and its related concepts. The main competency questions are: What is a power profile? What is an alternatives group? What is a power sequence? What is a slot? These questions are supported by the following statements:
- A power profile is a way to model curves of power and energy over time, which also provides definitions for the modelling of power scheduling including alternative plans. With a power profile, a device (or power sequences server) exposes the power sequences that are potentially relevant for the CEM (or power sequences client).
- An alternatives group is a collection of power sequences for a certain power profile.
- A power sequence is the specification of a task, such as wash or tumble dry, according to user preferences and/or manufacturer's settings for a certain device. It is the most 'coarse' view; a power sequence can represent all single steps of a whole task, where the single steps are represented by slots.
- A slot is a single step of a power sequence. A slot is associated with a slot number (while a power sequence is associated with a power sequence identifier). The slot numbers of two power sequences should be considered independent from each other, i.e. slot number 7 of sequence 1 describes a different slot than slot number 7 of sequence 2. Therefore, a slot is only uniquely identified in combination with a sequence ID. 


## References

[1] Suárez-Figueroa, Mari Carmen, Asunción Gómez-Pérez, and Mariano Fernández-López. "The NeOn methodology for ontology engineering." Ontology engineering in a networked world. Springer, Berlin, Heidelberg, 2012. 9-34.

[2] Elena Simperl. 2009. Reusing ontologies on the SemanticWeb: A feasibility study. Data & Knowledge Engineering 68, 10 (2009), 905–925.

[3] Adolfo Lozano-Tello and Asunción Gómez-Pérez. 2004. Ontometric: A method to choose the appropriate ontology. Journal of database management 2, 15 (2004), 1–18.

[4] Heiner Stuckenschmidt, Christine Parent, and Stefano Spaccapietra. 2009. Modular ontologies: concepts, theories and techniques for knowledge modularization. Vol. 5445. Springer.

[5] NF Noy, DL McGuinness. Ontology development 101: A guide to creating your first ontology (2011). Stanford knowledge systems laboratory technical report KSL-01-05

[6] Protégé tool: https://protege.stanford.edu/

[7] Seydoux et al. IoT-O, a Core-Domain IoT Ontology to Represent Connected Devices Networks (EKAW 2016)

[8] Agarwal et al. Unified IoT ontology to enable interoperability and federation of testbeds (WF-IoT 2016)

[9] Gyrard et al. Building IoT based applications for Smart Cities: How can ontology catalogs help? (IEEE IoT Journal 2017) 


## Appendix for this section

A set of pointers to develop your first ontology:
- Protégé Tutorial [Horridge et al. 2011] – Design the Pizza ontology. Check if there is a more recent documentation. Documentation: http://mowl-power.cs.man.ac.uk/protegeowltutorial/resources/ProtegeOWLTutorialP4_v1_3.pdf
- 101 Ontology Development methodology [Noy et al. 2001] - Learn with the wine ontology and discover ontology best practices. Documentation: https://protege.stanford.edu/publications/ontology_development/ontology101.pdf

Ontology discovery: 
- LOV tool: http://lov.okfn.org/dataset/lov/
- LOV4IoT tool: http://lov4iot.appspot.com/?p=ontologies
- OpenSensingCity tool: http://ci.emse.fr/opensensingcity/ns/ontologies/
- Ready4SmartCities tool: http://smartcity.linkeddata.es/
 
Ontology Design Patterns (ODP) repository:
- http://www.ontologydesignpatterns.org 

Locality Module Extractor tool: 
- https://www.cs.ox.ac.uk/isg/tools/ModuleExtractor/ 
