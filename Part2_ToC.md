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

## Software Implementation [Sonia Bilbao, Charbel Kaed]
Give an overview of different aspects that are needed when writing software for processing semantic information.

//this part is taken from the OLGA paper, I need to reformulate later
We split the available libraries and frameworks in various programming languages for ontology-based development in two categories,
i.e., serializers and Object Relational Mappers (ORMs).

### Serializers

Serializers provide reading/writing from/to an ontology file, a SPARQL endpoint, or a persistent RDF store. RDF Serializers are implemented in various programming languages, such as [OWL API](https://github.com/owlcs/owlapi/wiki), [RDF4J](http://rdf4j.org), and [Jackson-Jsonld](https://github.com/io-informatics/jackson-jsonld) in Java, [dotNetRDF](http://www.dotnetrdf.org,) in
.Net, [Redland](librdf.org) in C, and [RDFLib](https://rdflib.readthedocs.io) in Python. The serializers’ APIs provide low level classes and functions to manipulate concepts directly mapped to the Rdf language without any higher level abstractions. Therefore, it is required by any IoT developer to be aware of the technical aspects and theory of the RDF concepts and principals in order to implement ontology-based IoT applications.
We discuss in the following the serializers offering basic code generation through a plugin which takes an ontology as an input
and generates some code facilitators or stubs. The [Protégé code generation plugin](https://github.com/protegeproject/code-generation), which can be easily integrated in [Protégé](http://protege.stanford.edu) provides generation of Java code based on the [OWL API](https://github.com/owlcs/owlapi/wiki). However, the code generation is partial where only the class name and interface are provided along with an empty constructor. Then, it is up to the developer to complete the generated code by relying on the OWL API which requires a learning curve since it is directly mapped to the RDF concepts.

The [RDF4J Schema generator](https://github.com/ansell/
rdf4j-schema-generator,) extends the RDF4J API and provides an automatic generation of an RDF schema from an
ontology. The generated output of the ontology is contained in one java file which contains only the IRI of each concept of the
ontology. In other words, the code generation is flat, there are no classes, associations, or constraints between the generated elements. It is up to the developer to implement the association, mapping, and constraints manually.
[AutoRDF](https://github.com/ariadnext/AutoRDF) extends the Redland library and proposes a generator which takes an ontology and generates C++ object oriented
code to manipulate RDF concepts. The generated code is an abstraction layer which consists in a set of functions based on the
ontology classes and relations available to be used by developers to generate ontology instances (A-Box).

### Object Relation Mappers (ORMs)
ORMs are built on top of serializers and provide an object oriented abstraction layer allowing developers to manipulate objects
instead of RDF concepts. Several ORMs are available in various programming languages, such as [KOMMA](http://iswc2011.semanticweb.org/fileadmin/iswc/Papers/Workshops/SWESE/6.pdf), [Empire](https://github.com/mhgrove/Empire) and
[AliBaba](https://bitbucket.org/openrdf/alibaba) in Java, [RomanticWeb](http://romanticweb.net/) and [TrinityRDF](https://bitbucket.org/semiodesk/trinity) in .Net, and [RDFAlchemy](https://github.com/gjhiggins/RDFAlchemy) in Python. ORMs rely on the code decoration
where a developer annotates her code with tags referencing IRIs from the ontology terminology (T-Box). Most of the Java ORM rely
on the [Java Persistence API (JPA)](http://www.oracle.com/technetwork/articles/javase/persistenceapi-135534.html) while the .Net ORMs rely on the [Entity Framework](https://github.com/aspnet/EntityFramework6). During the code implementation of
an application, the developer requests a factory to instantiate the ontology (A-Box) and can formulate SPARQL queries by relying on
SPARQL query builders or adapters such as the LINQ to SPARQL in the .Net domain.
We discuss in the following the ORMs providing some code generation features.

[AliBaba](https://bitbucket.org/openrdf/alibaba) offers the three following interesting features for ontology developers. a) The object server exposes the object factory
through a REST API putting the available objects as resources on the web for manual annotation. b) The aspect behaviors which
allow each object of the factory to intercept a method call and execute a specific behavior. Annotation such as precedes provides
the developer with a better control with the behavior execution flow. c) SPARQL queries decoration on the getter/setters of objects which enables dynamic queries execution. In fact, compared to other ORMs, this feature is similar to invoking SPARQL queries in
the implementation methods. AliBaba highlights a java code generator which seems to handle simple ontologies, it failed to generate
code when tested with the [SAREF](http://ontology.tno.nl/saref.ttl) ontology. AliBaba provides interesting concepts for ontology based development, however, it
is clearly targeting ontology and not IoT developers since RDF and SPARQL are part of its APIs and design.
KOMMA relies on the Eclipse Modeling Framework [EMF](eclipse.org/emf) and is inspired by AliBaba’s design. KOMMA provides a unified
framework with the following three layers: an object mapping persistence layer, visualization tool, and an ontology editor based on
the capabilities of the EMF. KOMMA mentions a code generator plugin, however, it is not integrated in visualization and editing
layers, therefore, the mapping and implementation of the interfaces remain manual. KOMMA’s unified approach clearly targets ontology
developers with the integration of the three layer in a common framework. A learning curve is expected from an IoT developer for
both the ontology editing and the object mapping which consists in decorating the code with concepts from the ontology.

In addition, [OLGA](https://ecostruxure.github.io/OLGA/) (an Ontology Library GenerAtor) is a multi-library code generator it takes
two parameters as input: one or more ontologies since an ontology can depend on other ontologies and a choice of a library dependency.
In fact, the generated library will depend either on a serializer or a an object relational mapper. Thus, OLGA completes already existing libraries and frameworks, those depicted previously by providing IoT developers with the variety of choice for the development of ontology-based IoT applications. OLGA enables the possibility for an IoT developer to choose and reuse existing open source libraries
(serializers or ORMs) while offering an abstraction and a simpler library to use which conforms to an ontology model previously
specified by the experts.

### Available frameworks in Java:
Jena (https://jena.apache.org/) is a free and open source Java framework for building Semantic Web and Linked Data applications. It provides several Jena sub-systems and APIs:
-	RDF API to create and read RDF graphs
-	ARQ: a query engine for Jena that supports the SPARQL RDF Query language. 
-	Fuseki (https://jena.apache.org/documentation/fuseki2/): a SPARQL server to expose your triples as a SPARQL end-point accessible over HTTP. It can run as an operating system service, as a Java web application (WAR file), and as a standalone server. 
-	Ontology API to work with models, RDFS and Web Ontology Language (OWL)
-	Inference API to reason over the data

### Code implementation
In order to write software for processing semantic information, the first thing we need to do is to set up a semantic repository where the models will be added. We will use Apache Jena Fuseki (https://jena.apache.org/documentation/fuseki2/) that provides a robust, transactional persistent storage layer and a SPARQL server.
-	Download the software from https://jena.apache.org/download/
-	Install and run Fuseki: https://jena.apache.org/documentation/fuseki2/fuseki-run.html 
From now on we will assume that the name of the dataset is “exampleds” and the dataset URI is http://localhost:3030/exampleds.

Next, we provide code to manage CRUD operations on semantic models and to query and update the datasets.

Code to add a model to the default graph of the dataset  and to replace the default model 
```
import org.apache.jena.query.*;
import org.apache.jena.rdf.model.*;
import java.io.*;
import java.util.*;
import org.apache.jena.update.*;

public void addModel(File rdf) throws IOException {
    // parse the ontology file
    Model newModel = ModelFactory.createDefaultModel();
    try (FileInputStream in = new FileInputStream(rdf)) {
        newModel.read(in, null, "RDF/XML");
    }
    
    DatasetAccessor accessor = DatasetAccessorFactory.createHTTP(“http://localhost:3030/exampleds”);
    // Add statements to the default model of a Dataset
    accessor.add(newModel);      
}

public void replaceModel(File rdf) throws IOException {
    // parse the ontology file
    Model m = ModelFactory.createDefaultModel();
    try (FileInputStream in = new FileInputStream(rdf)) {
        m.read(in, null, "RDF/XML");
    }
    
    DatasetAccessor accessor = DatasetAccessorFactory.createHTTP(“http://localhost:3030/exampleds”);
    // Replace the default model of a Dataset
    accessor.putModel(m);
}
```

Code to delete the default model of the dataset
```
public void deleteModel() throws IOException {
    DatasetAccessor accessor = DatasetAccessorFactory.createHTTP(“http://localhost:3030/exampleds”);
    accessor.deleteDefault();
}
```

Code to retrieve the default model of the dataset
```
public Model getModel() throws IOException {
    DatasetAccessor accessor = DatasetAccessorFactory.createHTTP(“http://localhost:3030/exampleds”);
    return accessor.getModel();
}
```

Code to query the dataset providing as input a string with a query in SPARQL syntax
```
public List<Map<String, Object>> queryModel(String sparqlQuery) {
    List<Map<String, Object>> mapResult = new ArrayList<>();

    try (QueryExecution qexec = QueryExecutionFactory.sparqlService(“http://localhost:3030/exampleds”, sparqlQuery)) {
        org.apache.jena.query.ResultSet results;
        results = qexec.execSelect();

        while (results.hasNext()) {
            QuerySolution soln = results.nextSolution();
            mapResult.add(DataAccessManager.createMap(soln));
        }
    }

    return mapResult;
}

private Map<String, Object> createMap(QuerySolution querySolution) {
    Map<String, Object> result = new HashMap<>();
    Iterator<String> it = querySolution.varNames();
    while (it.hasNext()) {
        String varName = it.next();
        if (querySolution.get(varName) instanceof Literal) {
            result.put(varName, querySolution.getLiteral(varName));
        } else {
            result.put(varName, querySolution.getResource(varName));
        }
     }
     return result;
}
```

Code to update (INSERT, DELETE) the dataset providing as input a string with a query in SPARQL Update language
```
public void updateModel(String sparqlQuery) {
    UpdateRequest update = UpdateFactory.create(sparqlQuery);
    UpdateProcessor processor = UpdateExecutionFactory.createRemote(update, “http://localhost:3030/exampleds”);
    processor.execute();
}
```

### Code implementation with OLGA 

OLGA example: https://github.com/EcoStruxure/OLGA/wiki/Hello-World


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
