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

This example describes how to represent metadata and observations from a Salinity Sensor sensing device using the Semantic Sensor Network [SSN] (https://www.w3.org/2005/Incubator/ssn/ssnx/ssn) ontology. 

The Salinity Sensor is a device that can measure the salinity of liquids. The SSN ontology defines the class ssn:SensingDevice as a sub class of ssn:Sensor as well as of ssn:Device. Hence, as salinity sensor is a type of sensing device it can be represented as a subclass of ssn:SensingDevice.
```
SalinitySensor rdfs:subClassOf ssn:SensingDevice
```

In order to define a concrete instance of a Salinity Sensor, we need to name it (e.g. SENS_WAT_SAL01) and define its type:
```
SENS_WAT_SAL01 rdf:type SalinitySensor
```

Next, we need to define what the sensing device observes. This relation between the sensing device and what it observes is done through a ssn:Property.
```
SENS_WAT_SAL01 ssn:observes salinityConcentration
salinityConcentration rdf:type ssn:Property
```

We can also define the range that the sensor can measure. In our case, the Salinity Sensor can measure the entire range from 0-50 ppt (parts per thousand). The SSN ontology can be used in conjunction with the DUL ontology to manage data.
```
SENS_WAT_SAL01 ssn:hasOperatingRange sal01SalinityOperatingRange
sal01SalinityOperatingRange rdf:type ssn:OperatingRange
sal01SalinityOperatingRange dul:hasRegion aSalinityRegion
aSalinityRegion rdf:type dul:Region
aSalinityRegion dul:hasRegionDataValue "0 +50ppt"
```

Once we have represented the metadata about the sensor, we can model its observations as instances of class ssn:Observation. For each sample we have the following information: a timestamp, a value and its units. For example, the salinity observation of 26.35 ppt taken on the 1st June 2018 at 09:25 by SENS_WAT_SAL01 would be modelled as:
sample1 rdf:type ssn:Observation

An observation is the result of estimating a value of a property of a feature using a sensing method implemented by a sensor. In our case, the feature is the water quality that can be measured through different properties being one of them the salinity concentration. In this case, we would say that the observation sample1 was observed by the sensor SENS_WAT_SAL01, which observed the salinity property in order to measure the water quality feature. 
```
sample1 ssn:observedBy SENS_WAT_SAL01
sample1 ssn:observedProperty salinityConcentration
sample1 ssn:featureOfInterest waterQuality
waterQuality rdf:type ssn:FeatureOfInterest
waterQuality ssn:hasProperty salinityConcentration
```

Finally, we need to represent the value of the measurement of the sample1 observation and the time stamp when the measurement was taken. The DUL ontology is used in combination with SSN for this purpose. Each measurement is related to its value through the ssn:observationResult property and to its timestamp through the ssn:observationResultTime property. The measurement is an instance of ssn:SensorOutput with a value of type ssn:ObservationValue whereas the timestamp can be modelled as an instance of dul:TimeInterval.
```
sample1 ssn:observationResult result1
result1 rdf:type ssn:SensorOutput
result1 ssn:hasValue sample1val1
sample1val1 rdf:type ssn:ObservationValue
sample1val1 dul:hasRegionDataValue "26.35"^^xsd:double

sample1 ssn:observationResultTime result1time
result1time rdf:type dul:TimeInterval
result1time dul:hasRegionDataValue "2018-06-01T09:25:12.010"^^xsd:dateTime
```

Other examples: 
- Markus Stocker provides an example in his post of representing metadata about the LI-7500 sensing device used for monitoring of CO2 and H2O fluxes. http://markusstocker.com/sensing-devices-and-their-metadata/
- An example of the SSN-XG sensor ontology used to describe the Vaisala WM30 sensing device which measures wind speed and wind direction. https://www.w3.org/2005/Incubator/ssn/ssnx/meteo/WM30 


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
