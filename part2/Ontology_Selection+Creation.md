# Ontology Selection / Creation [Amelie Gyrard, Iker Esnaola, Izaskun Fernandez]

Ontology Selection/Creation diagram:

![Ontology selection/creation diagram flow](https://image.ibb.co/d4iAxT/Diagram.png)

## Identify ontology requirements

First of all, it is necessary to think about the objectives of the ontology. For that purpose, filling an ORSD (Ontology Requirements Specification Document) may be helpful. It facilitates identifying why the ontology is being built, what its intended uses are, who the end users are, and which requirements the ontology should fulfill.

- ORSD guide: http://oa.upm.es/5474/1/INVE_MEM_2009_64393.pdf

## Reuse existing ontologies

Once the objectives of the ontology are clear, it is necessary to actually have an ontology that fulfills those objectives. Instead of creating an ontology from scratch, it is a good practice to reuse existing ontologies when possible due to the following reasons [2]:

- The sharing and reuse of ontologies increase the quality of the applications using them, as these applications become interoperable and are provided with a deeper, machine-processable and commonly agreed-upon understanding of the underlying domain of interest.
- It reduces the costs related to ontology development because it avoids the reimplementation of ontological components, which are already available on the Web and can be directly – or after some additional customization – integrated into a target ontology.
- It potentially improves the quality of the reused ontologies, as these are continuously revised and evaluated by various parties through reuse.

According to [2], ontology reuse can be understood as a three-step process: (i) ontology discovery, (ii) ontology selection, and (iii) ontology integration.

### (i) Ontology discovery 

It consists in finding appropriate ontologies that meet our requirements. This task can nowadays be facilitated due to the numerous ontology catalogs to find existing ontologies. The most popular are:
 
- Linked Open Vocabularies for Internet of Things (LOV4IoT) references more than 440 ontology-based projects relevant for IoT. It covers more than 20 domains: IoT, Wireless Sensor Networks (WSNs), Web of Things (WoT), smart home, smart energy, healthcare, smart city, robotics, etc. LOV4IoT is highly maintained and references more and more ontology-based projects and new domains are covered.
   
- OpenSensingCity, an ontology catalog for smart cities. This catalog might be not maintained anymore after the end of the project (ANR french project).
  
- Ready4SmartCities, an ontology catalog for smart cities. It seems it is not maintained anymore. 

- Linked Open Vocabularies (LOV) designed by the Semantic Web community. This catalog is highly maintained and references ontology fitting their best practices criteria (e.g., ontology metadata).

TO DO?:
We can reuse well-written paragraphs about ontology catalogs from this paper (third revision ongoing) if needed: Building IoT based applications for Smart Cities: How can ontology catalogs help? [Gyrard et al. IEEE IoT Journal 2017] (Impact Factor 7.5)

### (ii) Selection of suitable (parts of) ontologies

This task deals with assessing the usability of an ontology with respect to the use case requirements. This may end up being an arduous task due to the different criteria that may make ontologies suitable for a certain use case [3]. Furthermore, the scarce documentation of ontologies may difficult even more this process.

In order to ease this selection phase, we recommend to look first at ontologies supported by standardization activities (e.g., W3C SOSA, SAREF, W3C WoT, oneM2M, etc.).

In case the developer needs to reuse only a subset of classes and properties of the ontology, instead of the whole ontology, an extractor tool (see Appendix section) can be used.

Limitations: Indeed, we would need some ontology ranking algorithms to help better developers find suitable ontologies for their needs.

### (iii) Ontology integration 
Finally, the selected ontology or ontologies may need to be customized in order to adapt them and satisfy the use case’s requirements. This customization may involve additional modification and integration operations such as extraction of ontology parts or even content and structural modification or extension.

When more than one ontology (or parts) are integrated, ontology matching tool can be performed to return a potential alignment between two ontologies. Some basic ontology matching tasks consist in setting relationships such as:
- Equivalences between concepts (with the owl:equivalentClass property)
- Subsumptions (with the rdfs:subClassOf or rdfs:subPropertyOf properties)
- Disjointness between entities (with the owl:DisjointOf property)
- Labels an comments to deduce similarities (with rdfs:label and rdfs:comment properties)

## Create new ontology / Extend existing ontologies

If the existing ontologies do not meet all the requirements captured in the OSRD, ontologies need to be extended. 

In case no existing ontologies have been found for our specific requirements captured in the OSRD, there might be a need to develop your own ontology. 

For a more exhaustive ontology creation guide, we advice excellent documentation and methodologies: the NeOn methodology for ontology engineering[1], and the ontology development 101 [5]).

Protégé [6] is one of the most popular software to learn how to create ontologies. Protégé provides a Graphical User Interface (GUI) to design and develop ontologies. You can either set up Protege on your computer or use the web collaborative Protege tool. We provide a set of excellent tutorials to develop your first ontology with Protégé (see Appendix Section.

When creating or extending an ontology, it is advisable to follow the modularisation principle by separating the required knowledge in well-decoupled ontology modules. The main benefits of this principle are: 1) scalability for querying data and reasoning on ontologies, 2) scalability for evolution and maintenance, 3) complexity management, 4) understandability, 5) context-awareness and personalization, and 5) reuse [4]. For example, when some of the ontology modules are updated, thanks to the modularization, the impact of these changes in other modules and the global ontology is minimized. IoT-O [7] and [8] FIESTA-IoT ontologies are good examples of ontology modules.

It is also recommendable to use Ontology Design Patterns (ODP) (see Appendix Section) as building blocks to create new ontology modules. An ODP is a modeling solution to solve a recurrent ontology design problem. The ODP repository collects and makes ODPs available on the web. It may contain a solution created by somebody else who already faced the same modeling challenge.

Once the ontology is created, it is advisable to align it with related ontologies and upper-level ontologies (i.e. DUL) to make the ontology applicable to similar problems in different domains and scenarios.

TO DO? should we provide more examples protege with smart home ontology? How to create a concept, and property relevant for smart home (show protege interface, and code)?

TO DO? Check and merge with ontology development section (Part2.md)?

## Ontology Selection
Most of the time you already have some keywords and key phrases in mind to build the system or application. For the smart domain, keywords are “room temperature” “actuators”, “humidity”, those keywords can be mapped to concepts within ontologies.
Ontology catalogs can provide such browsing functionalities with specific keywords.


## References

[1] Suárez-Figueroa, Mari Carmen, Asunción Gómez-Pérez, and Mariano Fernández-López. "The NeOn methodology for ontology engineering." Ontology engineering in a networked world. Springer, Berlin, Heidelberg, 2012. 9-34.

[2] Elena Simperl. 2009. Reusing ontologies on the SemanticWeb: A feasibility study. Data & Knowledge Engineering 68, 10 (2009), 905–925.

[3] Adolfo Lozano-Tello and Asunción Gómez-Pérez. 2004. Ontometric: A method to choose the appropriate ontology. Journal of database management 2, 15 (2004), 1–18.

[4] Heiner Stuckenschmidt, Christine Parent, and Stefano Spaccapietra. 2009. Modular ontologies: concepts, theories and techniques for knowledge modularization. Vol. 5445. Springer.

[5] NF Noy, DL McGuinness. Ontology development 101: A guide to creating your first ontology (2011). Stanford knowledge systems laboratory technical report KSL-01-05

[6] Protégé tool: https://protege.stanford.edu/

[7] Seydoux et al. IoT-O, a Core-Domain IoT Ontology to Represent Connected Devices Networks (EKAW 2016)

[8] Agarwal et al. Unified IoT ontology to enable interoperability and federation of testbeds (WF-IoT 2016)


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
