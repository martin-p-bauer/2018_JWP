# Part 2

## Overall Guidance 
Target Audience: Developers, System Architects

Goal: Show how to implement semantic solutions and to achieve semantic interoperability

Give an overview of strengths when using semantic technologies.

Abstractions, hiding some aspects to make applications easier (but keeping key advantages).

Introduce existing tools, how they can be applied.

Point to relevant standard.

Show a small, but relevant example, e.g. cross-domain.

## Introduction
The Internet of Things (IoT) is expected to interconnect, at massive
scale, numerous sensors, devices, gateways, and systems to tackle
many challenges in the industry. 

Such inter-connectivity will
play an essential part in designing industrial systems with added
value services which are more energy efficient with lower costs
while contributing to a better environment. These promises promoted
by the emergence of the industrial Internet of Things have surged the importance of interoperability among the things
to turn this vision into reality.
Designing IoT applications requires a shared understanding of
the exchanged data among those connected things. Semantic technology,
is one of the most promising fields in the knowledge representation
domain, expected to enable interoperability in the IoT.
TheWorld WideWeb Consortium (W3C) defines a set of standards ,
such as RDF, OWL, JSON and SPARQL, to represent semantics
and query linked data, offering an ideal ecosystem and opportunity
to tackle the heterogeneity challenge in the IoT. In industrial environments
and automation domains, semantic technology has been
used to solve data/Device interoperability issues and to provide
context aware applications and services.

Despite its potential and promises, semantic technology and
ontology-based IoT applications still remain in the hands of a minority,
the ontology experts, being too difficult to be adopted and
applied by industrial practitioners. We attribute such retention
among other factors to the absence of adequate methodology and
tools involving several major actors participating in the design life cycle
of an IoT application, who are typically non-ontology experts.

## Problem
The W3C defined a semantic layer cake (citation https://www.w3.org/2000/Talks/1206-xml2k-tbl/slide10-0.html) based on a set of standards to develop the semantic web. The aim of these standards is to focus mainly on the knowledge representation to solve the data interchange problem in addition to several non functional requirements such as data validation, proof and trust.

**Insert semantic layer cake image here**

According to the Semantic Web standards, data representation can be expressed in the following standards RDF, RDF-S, and OWL. More precisly, such descriptive languages allow to represent a model and its instantiation. Several ontologies exist publically to represent a domain model, for example: the Semantic Sensor Network Ontology (https://www.w3.org/TR/vocab-ssn/) proposes a model to represent a sensor network, SAREF (Documentation:http://ontology.tno.nl/saref; URL:http://ontology.tno.nl/saref.ttl) proposes a model to represent smart appliances functionalities, expected behavior and how they interact with their environment and their locations. Other ontologies such as Brick (citation) focus on the Building Management System domain detailing a vocabulary of equipment types, their expected behviour in addition to their interactions with other equipments.

Once an ontology model has been defined, the next step is to instantiate it. Instantiating an ontology implies producing data which conforms to the model. For example, an instantiation of a Brick ontology implies for a given site, the data produced by a Building Management System conforms to the Brick Model. **(need to give a simple example here based on a public ontology, maybe Brick is not so generic, to be discussed on the call)**
* http://www.cs.virginia.edu/~dh5gm/pdf/brick-journal.pdf
* https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=8&cad=rja&uact=8&ved=0ahUKEwjG4_j-3onbAhUxb5oKHbj_BjUQFghCMAc&url=https%3A%2F%2Fbrickschema.org%2Fpapers%2FBrick_BuildSys_Presentation.pdf&usg=AOvVaw1igBB2grS0-9uMXD2_9kPW

Ontology instantiation process requires:
1. An ontology model.
2. A software enabler to produce or transform data according to the provided ontology model.
3. A software developer implementing the software enabler

Acceptance criteria:
1. Data produced conforms to the ontology model
2. Data produced is expressed in one of the W3C standards formats such as rdf/xml, json-ld, citations.

**Should we give an overview of the Software Developer persona?**
A Software Developer persona is a non ontology expert, non familiar with the Semantic Layer cake. She is given an ontology model expressed in OWL and is asked to develop an enabler which can be embedded in a system or on the cloud to produce (or transform) data conform to the model. The data produced need to be expressed in one of the W3C standard.

In the following, we depict the list of tools available to a software developer to achieve her goal and meet the acceptance criteria 


** Focus on Developer Experience: NON Ontology Expert **

## Existing Methods and Tools

### Ontology Html Renderers
#### General overview of their usage and functions
1. [Ontoology](http://ontoology.linkeddata.es/) with [detailed instructions](http://ontoology.linkeddata.es/stepbystep) on how to use it.
2. [LODE](https://github.com/essepuntato/LODE)

   LODE Web Service example: http://www.essepuntato.it/lode/http://purl.org/iot/ontology/fiesta-iot#

### Visual Modeling Tools
#### General overview of their usage and functions

#### List Some
1. Protégé
2. TopBraid Composer
3. Ontology Visualization with WebVOWL

   WebVOWL Web Service example:
  
   http://visualdataweb.de/webvowl/#iri=http://purl.org/iot/ontology/fiesta-iot#

4. Others?

### Serializers APIs
#### General overview of their usage and functions
#### List Some
1. OWL API (Java)
2. RDF4J (Java)
3. DotNetRDF (C#)
4. RDF Charm (Python)
5. json module (Python)
6. RDFLib (Python)

#### Semantic Web and Linked Data application building open source
#### General overview of their usage and functions
#### List Some
1. Apache Jena (Java)

#### Semantic repository/database/store
#### General overview of their usage and functions
#### List Some
1. Sesame (Java)
2. MongoDB (C++, Java and Python drivers)
3. Jena TDB
4. OpenLink Virtuoso
5. OWLIM
6. Oracle Spatial and Graph RDF Semantic Graph

### Retrieving Semantic Information
1. SPARQL (expressive query language on general RDF data, but requires (logically) centralized information)
2. NGSI-LD (retrieve scopded and filtered information, entity meta model, also works in highly distributed and federated settings)
   * Overview presentation: https://docbox.etsi.org/ISG/CIM/Open/Introduction_NGSI-LD_20180413.pdf
   * ETSI Group Specification: http://www.etsi.org/deliver/etsi_gs/CIM/001_099/004/01.01.01_60/gs_CIM004v010101p.pdf 

### Object Relational Mappers
#### General overview of their usage and functions
#### List Some
1. RomanticWeb (C#)
2. TrinityRDF (C#)
3. Empire (Java)
4. [Pinto](https://github.com/stardog-union/pinto)
5. [Komma](https://github.com/komma/komma)
6. Others?

### Code Generators
#### General overview of their usage and functions
#### List Some
1. Protégé Plugin
2. Eclipse EMF
3. [OLGA](https://www.researchgate.net/publication/319650390_A_Model_Driven_Approach_Accelerating_Ontology-based_IoT_Applications_Development): Ontology Library Generator 

### Ontology Alignment APIs?

1. LogMap

  LogMap Web Service: http://krrwebtools.cs.ox.ac.uk/logmap/

## What is missing ? (need to find a better title here)

PerfectO project - Ontology Improvement Tool integrating a set of tools mentionned previously (WebVOWL, LODE, LogMap, etc.):

Demo: http://perfectsemanticweb.appspot.com/?p=ontologyValidation
