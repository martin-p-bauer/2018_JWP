# Ontology Selection / Creation [Amelie Gyrard, Iker Esnaola, Izaskun Fernandez]

(For a more exhaustive Ontology creation guide, go to [1] [5]).

First of all, it is necessary to think about the objectives of the ontology. 

- Ontology Requirements Specification Document (ORSD). Facilitates identifying why the ontology is being built, what its intended uses are, who the end users are, and which requirements the ontology should fulfill (Guide: http://oa.upm.es/5474/1/INVE_MEM_2009_64393.pdf )

Never start from scratch. It is a big no-no in the ontology engineering. A good practice is to reuse existing ontologies when possible.

## How to reuse existing ontologies?

According to [2], ontology reuse can be understood as a three step process: (i) ontology discovery, (ii) ontology selection, and (iii) ontology integration.

(i) Ontology discovery consists in finding appropriate ontologies for the desired topic. This task can be nowadays facilitated due to the existing semantic web search engines like Watson. There are numerous ontology catalogs to find existing ontologies. The most popular are:
- Linked Open Vocabularies (LOV) designed by the Semantic Web community. This catalog is highly maintained and references ontology fitting their best practices criteria (e.g., ontology metadata).
 
  LOV tool: http://lov.okfn.org/dataset/lov/

- Linked Open Vocabularies for Internet of Things (LOV4IoT) references more than 440 ontology-based projects relevant for IoT. It covers more than 20 domains: IoT, Wireless Sensor Networks (WSNs), Web of Things (WoT), smart home, smart energy, healthcare, smart city, robotics, etc. LOV4IoT is highly maintained and references more and more ontology-based projects and new domains are covered.
  
  LOV4IoT tool: http://lov4iot.appspot.com/?p=ontologies

- OpenSensingCity, an ontology catalog for smart cities. This catalog might be not maintained anymore after the end of the project (ANR french project).
  
  OpenSensingCity tool: http://ci.emse.fr/opensensingcity/ns/ontologies/

- Ready4SmartCities, an ontology catalog for smart cities. It seems it is not maintained anymore. 
  
  Ready4SmartCities tool: http://smartcity.linkeddata.es/

(ii) The ontology selection task deals with assessing the usability of an ontology with respect to the use case requirements. This may end up being an arduous task due to the different criteria that may make ontologies suitable for a certain use case [3]. Furthermore, the scarce documentation of ontologies may difficult even more this process.

We recommend to look first at ontologies supported by standardizations (e.g., W3C SOSA, SAREF, W3C WoT, ONeM2M, etc.).

Limitations: Indeed, we would need some ontology ranking algorithms to help better developers find suitable ontologies for their needs.

(iii) Finally, the selected ontology or ontologies may need to be customized in order to adapt them and satisfy the use case’s requirements. This customization may involve additional modification and integration operations such as extraction of ontology parts or even content and structural modification or extension.

In case the developer needs to reuse only a subset of classes and properties of the ontology:

- Locality Module Extractor tool: https://www.cs.ox.ac.uk/isg/tools/ModuleExtractor/ 

Furthermore, if the existing ontologies does not meet all the requirements explicated in the OSRD, they need to be extended. For that purpose, it is advisable to separate the required knowledge in well-decoupled ontology modules which has in benefits: scalability for querying data and reasoning on ontologies; scalability for evolution and maintenance; complexity management; understandability; context-awareness and personalization; and reuse [4]. For example, when some of the ontology modules is updated, thus minimizing this way the impact of these changes in other modules and the global ontology.

It is also recommendable to use Ontology Design Patterns (ODP) as building blocks to create new ontology modules. An ODP is a modelling solution to solve a recurrent ontology design problem. The ODP repository collects and makes ODPs available on the web. It may contain a solution created by somebody else who already faced the same modelling challenge 

- ODP Repository: http://www.ontologydesignpatterns.org 

Once the ontology is created, it is advisable to align it with related ontologies and upper-level ontologies (i.e. DUL) to make the ontology applicable to similar problems in different domains and scenarios.

Comments:
We can reuse well-written paragraphs about ontology catalogs from this paper (third revision ongoing) if needed: Building IoT based applications for Smart Cities: How can ontology catalogs help? [Gyrard et al. IEEE IoT Journal 2017] (Impact Factor 7.5)

## How to extend ontologies?
TO DO

Import ontologies

Reuse ontology namespace

show concrete code example?

## How to create ontologies?
Protege is one of the most popular software to learn how to create ontologies. Protégé provides a Graphical User Interface (GUI) to design and develop ontologies. You can either set up Protege on your computer or use the web collabative Protege tool.

Protege tool: https://protege.stanford.edu/

A set of pointers to develop your first ontology:
- Protégé Tutorial [Horridge et al. 2011] – Design the Pizza ontology. Check if there is a more recent documentation.
  
  Documentation: http://mowl-power.cs.man.ac.uk/protegeowltutorial/resources/ProtegeOWLTutorialP4_v1_3.pdf
  
- 101 Ontology Development methodology [Noy et al. 2001] - Learn with the wine ontology and discover ontology best practices.
  
  Documentation: https://protege.stanford.edu/publications/ontology_development/ontology101.pdf


TO DO: Check and merge with ontology development section (Part2.md)?

## References

[1] Suárez-Figueroa, Mari Carmen, Asunción Gómez-Pérez, and Mariano Fernández-López. "The NeOn methodology for ontology engineering." Ontology engineering in a networked world. Springer, Berlin, Heidelberg, 2012. 9-34.

[2] Elena Simperl. 2009. Reusing ontologies on the SemanticWeb: A feasibility study. Data & Knowledge Engineering 68, 10 (2009), 905–925.

[3] Adolfo Lozano-Tello and Asunción Gómez-Pérez. 2004. Ontometric: A method to choose the appropriate ontology. Journal of database management 2, 15 (2004), 1–18.

[4] Heiner Stuckenschmidt, Christine Parent, and Stefano Spaccapietra. 2009. Modular ontologies: concepts, theories and techniques for knowledge modularization. Vol. 5445. Springer.

[5] NF Noy, DL McGuinness. Ontology development 101: A guide to creating your first ontology (2011). Stanford knowledge systems laboratory technical report KSL-01-05
