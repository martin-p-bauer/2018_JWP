# Overall Guidance
Target Audience: Developers, System Architects

Goal: Show how to implement semantic solutions and to achieve semantic interoperability

Give an overview of strengths when using semantic technologies.

Abstractions, hiding some aspects to make applications easier (but keeping key advantages).

Introduce existing tools, how they can be applied.

Point to relevant standard.

Show a small, but relevant example, e.g. cross-domain.

# Introduction [???]
High-level introduction regarding semantics and purpose of this paper (also see: overall guidance above). The idea is to show developers and system architects how to implement semantic solutions. The focus of the main paper is on the different activities. We show examples of tools there, but refer to the appendix for a more detailed description of further available tools.

# Problem Description [Michelle Wetterwald]
Describe the problem space in which semantics can be applied in more detail.

# Example Use Case [Laura Daniele]
Describe an example use case that instantiates the problem space, is as simple as possible, but shows the advantages of semantics and can be used in the following subsections.

# Ontology Selection / Creation [Amelie Gyrard]
How to find suitable ontologies and if necessary extend or create ontologies.

## How to find suitable ontologies?

There are numerous ontology catalogs to find existing ontologies. The most popular are:
- Linked Open Vocabularies (LOV) designed by the Semantic Web community. This catalog is highly maintained and references ontology fitting their best practices criteria (e.g., ontology metadata).
 
  LOV tool: http://lov.okfn.org/dataset/lov/

- Linked Open Vocabularies for Internet of Things (LOV4IoT) references more than 440 ontology-based projects relevant for IoT. It covers more than 20 domains: IoT, Wireless Sensor Networks (WSNs), Web of Things (WoT), smart home, smart energy, healthcare, smart city, robotics, etc. LOV4IoT is highly maintained and references more and more ontology-based projects and new domains are covered.
  
  LOV4IoT tool: http://lov4iot.appspot.com/?p=ontologies

- OpenSensingCity, an ontology catalog for smart cities. This catalog might be not maintained anymore after the end of the project (ANR french project).
  
  OpenSensingCity tool: http://ci.emse.fr/opensensingcity/ns/ontologies/

- Ready4SmartCities, an ontology catalog for smart cities. It seems it is not maintained anymore. 
  
  Ready4SmartCities tool: http://smartcity.linkeddata.es/

We recommend to look first at ontologies supported by standardizations (e.g., W3C SOSA, SAREF, W3C WoT, ONeM2M, etc.).

Limitations: Indeed, we would need some ontology ranking algorithms to help better developers find suitable ontologies for their needs.


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


# Ontology Instantiation [Charbel Kaed]
Given an ontology, how can this ontology be instantiated for a concrete use case.

# Software Implementation [Sonia Bilbao, Charbel Kaed]
Give an overview of different aspects that are needed when writing software for processing semantic information.

## Semantic Information / Semantic Annotation [???]
How to get to semantic information, e.g. based on original raw sensor data.

## Storing Semantic Information [Aitor Corchero Rodiguez]
How to store semantic information, making it accessible for later processing.

## Retrieving Semantic Information [Martin Bauer]
How to enable retrieving semantic information.

## Analytics and Reasoning using Semantic Information [???]
How to do analytics and reasoning using semantic information.

# Semantic Interoperability Across Systems [Antonio Jara]
How to achieve semantic interoperability across systems.

# Appendix: Existing Methods and Tools

## Ontology Html Renderers [???]

## Visual Modeling Tools [???]

## Serializers APIs [???]

## Semantic Web and Linked Data application building open source [???]

## Semantic repository/database/store [???]

## Retrieving Semantic Information [???]

## Object Relational Mappers [???]

## Code Generators [???]

## Ontology Alignment APIs? [???]
