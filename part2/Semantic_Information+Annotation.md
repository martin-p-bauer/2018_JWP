# Semantic Information & Semantic Annotation [Wenbin Li, Hamza Baqa]

Semantical information can help to bridge the different knowledge representations. As shown in the previous sections, it can be used to discover matching between models elements, which helps information systems integration. In our smart home energy use case, we use ontology objects for enriching Resource’s information, relevant information is about devices, their state, measurements and energy profiles.

To fully use semantic technologies, systems and platforms are expected to serve information with ontologies so that one can look up data content and get information from ontology definitions including the relationships between the terms in the ontology. Semantic information is regarded as any form of information containing explicit semantic descriptions and using ontologies to drive the information lifecycle. Comparing to classical syntax data, semantic information is human&machine understandable and unambiguous to support advanced data functions such as complex query, intelligent human-machine interaction, contextual data analytics and data interoperability. 

In order to have semantic information on hand, we have typically two ways, i.e., Semantic Information Creation and Semantic Annotation, as detailed as follows. Both of the processes bridge the gap between syntax and semantics world with different application cases. 

**Semantic Information Creation** produces semantic information using ontologies from scratch following specific serialization formats. The used ontologies specify the concepts and relations used in the information while the serialization formats define the semantic information structure. 

This is the most convenient way to create new semantic data based on semantic technologies, if no existing constraints apply. The semantic information built from scratch fully inherits the semantic benefits, while the required efforts are similar to the efforts of data creation following predefined schemas. 

**Semantic Annotation** is the process of linking existing syntax information with specific ontologies to provide both machine understandable and human readable descriptions, while the source information can be structured document, services, functions, metadata of image and videos, etc. Ontologies provide semantics to existing data and furthermore link different information together via predefined relations. 

This process is more suitable to the cases where data already exist based on other specifications or the data sources can only provide data following specific formats without semantics. Thus, the objective is to evolve the existing data with semantic technologies while keeping as much as possible the backward compatibility with existing specifications. 
In order to better illustrate the two process, we present an example following our smart home scenario, in which a room with an id room1001 and an energy limit profile is equipped with a temperature sensor providing temperature measurement and a washing machine providing washing machine with states and remote washing services to turn on/off and switch mode. We respectively introduce how we can build semantic information of the example following semantic information creation and semantic annotation; throughout the process, the main ontologies we use for semantic annotation are SAREF and SAREF4ENER, which are introduced in previous chapters.  

**1. Semantic Information Creation**
The semantic information creation builds the corresponding information from scratch. The general semantic information creation can be briefly summarized into the two following steps: 

1) Identification or definition of ontologies to be used; 
2) creation of semantic information by use of ontology concepts; 

In our example, we start to describe the room1001 resource is a type of Room defined in schema ontology, (since the Room type is not defined in SAREF or SAREF4ENER), and the Room1001 has an energy profile which points to another resource “/Limit”.  We use the standard N-Triples as the serialization format and the output of the above descriptions are three triples as. 
```
	Room1001 	rdf:type 		schema:Room,
	Room1001	saref4ener:hasEnergy 	/Limit,
	"/Limit"	rdf:type		saref4ener:energyMax
```
By doing so, we indicate that the Room1001 is an instance of the schema:Room class. The relation between the Room1001 and the resource “/Limit” is further detailed in the saref4ener:hasEnergy property, and the resource “/Limit” is actually an instance of the saref4ener:energyMax class which specifies the maximum energy profile. 
Secondly, we describe that the Room1001 has two devices with ids ts001 and wm002, which are respectively instances of saref:TemperatureSensor and saref:WashingMachine classes. 
```
	Room1001 	saref4ener:hasDevice	ts001,
	Room1001	saref4ener:hasDevice	wm002,
	ts001		rdf:type 		saref:TemperatureSensor,
	wm002		rdf:type 		saref:WashingMachine"
```
In the above information, the relations between Room1001 and two devices are further specified by saref4ener:hasDevice. 
As the last step, we further add the descriptions of the two devices we just added. 
```
	ts001		saref:hasValue		"25", 
	wm002		saref:hasState		wm002/state
	wm002/state	 rdf:type 		saref:State
	wm002		saref:offers		wm002/switch
	wm002/switch	rdf:type		saref:Service
```
In the above information, we actually describe that the temperature sensor ts001 has a sensed value 25; the washing machine wm002 has a state defined in wm002/state (an instance of saref:State class) and offers a switch service defined in wm002/switch (an instance of saref:Servuce class).
By combining all the triples above, we get the complete description of our example following semantic information creation process. Thorough the whole process, we also link different information together by use of the properties defined in different ontologies, which further facilitates the data search and analytics.  
Moreover, although we use N-triples as the serialization format in our example, the information we created can be easily transformed to other semantic serialization formats such as JSON-LD and RDF/XML. 

**2. Semantic Annotation**
Existing syntax information can be enriched with semantics and transformed to semantic information via semantic annotation. The general semantic process can be briefly summarized into the three following steps 
1) Preparation of source information to be annotated; 
2) Identification or definition of ontologies to be used; 
3) Manual or automatic link between source information to ontologies; 

Semantic annotations are widely used in various data-centric domains. The description of the rooms is serialized in JSON as presented below. 
```
{	"id": "room1001",
	"type": "Room",
	"energyProfile": "/Limit",
	"devices": [{	"id": "ts001",
			"type": "TemperatureSensor",
			"value": "25"},
		       {	"id": "wm002",
			"type": "WashingMachine",
			"state": "/state",
			"service": /switch"    }]
}
```
The JSON description of the Room1001 is the source information to be annotated. 
Starting from the general terms, we need to map the general terms “id” and “type” to JSON-LD node identifier and RDF type concept.    
```
	"id": "@id",
	"type": "rdf:type"
```
so that all ids in the JSON descriptions are defined as an object node with an URI as identifier, while all thing types are further linked as a type of an ontology class. 
In the following, all type targets in the JSON are mapped to different SAREF4ENER, except that we use the schema ontology to annotate the type of Room which is not defined in SAREF or SAREF4ENER. 
```
 	"TemperatureSensor": "saref:TemperatureSensor",
	"WashingMachine": "saref:WashingMachine",
	"Room": "schema:Room"
```
At last, we link the energyProfie, sensingValue, state and services with SAREF and SAREF4ENER concepts, 
```
	"energyProfile":"saref4ener:hasEnergy",
	"/Limit":"saref4ener:energyMax",
	"value":"saref:hasValue",
	"service": "saref:offers",
	"devices":"saref4ener:hasDevice",
	"wm002/switch": "saref:Service",
	"state ": "saref:hasState",
	"wm002/state": "saref:State"
```
At the of the annotation, all terms used in JSON are linked to semantic concepts, for example now we know that the resource "wm002/switch" is a device service defined by SAREF, and the "/Limit" is a resource describing the maximum energy consumption as specified in SAREF4ENER. 
The final serialization formats of the semantic annotation are rather flexible and can be formatted as with all semantic formats such as triples, JSON-LD, RDF/XML, etc. One convenient way for JSON document is to use JSON-LD to serialize the semantic annotation result, as we only need to add an extra field of “@conext” at the top of existing JSON which contains all previously defined mappings. 
```
	{	"@context": {
			"id": "@id",
			"wm002/state": "saref:State",
			… …
		},
		"id": "room1001",
		"type": "Room", 
		… …
	}
```
Here follows a sample of semantic annotation result based on triples format, 
```
	Room1001 	rdf:type 		"schema:Room",
	Room1001	saref4ener:hasEnergy 	"/Limit",
	"/Limit" 	rdf:type 		"saref4ener:energyMax",
… …
```

** 3. Other examples** 
- Markus Stocker provides an example in his post of representing metadata about the LI-7500 sensing device used for monitoring of CO2 and H2O fluxes. http://markusstocker.com/sensing-devices-and-their-metadata/
- An example of the SSN-XG sensor ontology used to describe the Vaisala WM30 sensing device which measures wind speed and wind direction. https://www.w3.org/2005/Incubator/ssn/ssnx/meteo/WM30
- A typical design of semantic annotation framework can be found in, https://www.researchgate.net/publication/319036946_Towards_a_Semantics_Extractor_for_Interoperability_of_IoT_Platforms








----------------------Old Version Below-----------------------------------------------------------------



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

