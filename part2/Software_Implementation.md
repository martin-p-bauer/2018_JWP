# Software Implementation [Sonia Bilbao, Charbel Kaed]

//this part is taken from the OLGA paper, I need to reformulate later
We split the available libraries and frameworks in various programming languages for ontology-based development in two categories,
i.e., serializers and Object Relational Mappers (ORMs).

## Serializers

Serializers provide reading/writing from/to an ontology file, a SPARQL endpoint, or a persistent RDF store. RDF Serializers are implemented in various programming languages, such as [OWL API](https://github.com/owlcs/owlapi/wiki), [RDF4J](http://rdf4j.org), and [Jackson-Jsonld](https://github.com/io-informatics/jackson-jsonld) in Java, [dotNetRDF](http://www.dotnetrdf.org,) in
.Net, [Redland](librdf.org) in C, and [RDFLib](https://rdflib.readthedocs.io) in Python. The serializers’ APIs provide low level classes and functions to manipulate concepts directly mapped to the Rdf language without any higher level abstractions. Therefore, it is required by any IoT developer to be aware of the technical aspects and theory of the RDF concepts and principles in order to implement ontology-based IoT applications.
We discuss in the following the serializers offering basic code generation through a plugin which takes an ontology as an input
and generates some code facilitators or stubs. The [Protégé code generation plugin](https://github.com/protegeproject/code-generation), which can be easily integrated in [Protégé](http://protege.stanford.edu) provides generation of Java code based on the [OWL API](https://github.com/owlcs/owlapi/wiki). However, the code generation is partial where only the class name and interface are provided along with an empty constructor. Then, it is up to the developer to complete the generated code by relying on the OWL API which requires a learning curve since it is directly mapped to the RDF concepts.

The [RDF4J Schema generator](https://github.com/ansell/
rdf4j-schema-generator,) extends the RDF4J API and provides an automatic generation of an RDF schema from an
ontology. The generated output of the ontology is contained in one java file which contains only the IRI of each concept of the
ontology. In other words, the code generation is flat, there are no classes, associations, or constraints between the generated elements. It is up to the developer to implement the association, mapping, and constraints manually.
[AutoRDF](https://github.com/ariadnext/AutoRDF) extends the Redland library and proposes a generator which takes an ontology and generates C++ object oriented
code to manipulate RDF concepts. The generated code is an abstraction layer which consists in a set of functions based on the
ontology classes and relations available to be used by developers to generate ontology instances (A-Box).

## Object Relation Mappers (ORMs)
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


## OLGA: an Ontology Library Generator
OLGA (Ontology Library GenerAtor) is a generic tool aiming to accelerate the adoption of [Standard W3C Semantic technology](https://www.w3.org/standards/semanticweb/) among developers. 

OLGA provides a better development experience by focusing on:

* Reducing friction barrier for developers when working with an ontology model.

* Accelerating development of ontology based systems.

* Eliminating complexity by providing Object Oriented libraries for developers.

OLGA is based on a model driven approach taking as input an ontology file expressed in one of the supported W3C supported standards ([RDF](https://www.w3.org/2001/sw/wiki/RDF), [OWL](https://www.w3.org/OWL)) and generating a library conform to the ontology model.

The generated library is then imported and used to programmatically to:
1. Generate an ontology instance conform to the ontology model.
2. Query the generated ontology instance by relying on Object Oriented Model instead of [SPARQL](https://www.w3.org/TR/sparql11-query/).

In fact, the generated library will depend either on a serializer or a an object relational mapper. Thus, OLGA completes already existing libraries and frameworks, those depicted previously by providing IoT developers with the variety of choice for the development of ontology-based IoT applications. OLGA enables the possibility for an IoT developer to choose and reuse existing open source libraries
(serializers or ORMs) while offering an abstraction and a simpler library to use which conforms to an ontology model previously specified by the experts.


# do we need to keep all the below? or it should go in the appendix?

## Available frameworks in Java:
Jena (https://jena.apache.org/) is a free and open source Java framework for building Semantic Web and Linked Data applications. It provides several Jena sub-systems and APIs:
-	RDF API to create and read RDF graphs
-	ARQ: a query engine for Jena that supports the SPARQL RDF Query language. 
-	Fuseki (https://jena.apache.org/documentation/fuseki2/): a SPARQL server to expose your triples as a SPARQL end-point accessible over HTTP. It can run as an operating system service, as a Java web application (WAR file), and as a standalone server. 
-	Ontology API to work with models, RDFS and Web Ontology Language (OWL)
-	Inference API to reason over the data

## Code implementation
Next we will show how to write software in Java for processing the semantic information from the previous power profile instantiation example.

The power profile uses the SAREF4ENER extension of SAREF ontology. So, the first thing we need to do is to set up a semantic repository where these models will be added. We will use Apache Jena Fuseki (https://jena.apache.org/documentation/fuseki2/) that provides a robust, transactional persistent storage layer and a SPARQL server.
-	Download the software from https://jena.apache.org/download/
-	Install and run Fuseki: https://jena.apache.org/documentation/fuseki2/fuseki-run.html 
From now on we will assume that the name of the dataset is “energyds” and the dataset URI is http://localhost:3030/energyds.

In order to add a model to the dataset we need to provide the path or url to the file and the RDF I/O technology (RIOT), e.g. Turtle, RDF/XML, etc. as shown below. The loadEnergyExample method shows how to add [SAREF4ENER](http://ontology.tno.nl/saref4ener.ttl), [SAREF](http://ontology.tno.nl/saref.owl) and the power profile instantiation to the dataset. The file [example.ttl](https://github.com/martin-p-bauer/2018_JWP/blob/master/part2/example.ttl) contains the RDF code for the power profile. SAREF4ENER is in Turtle format whereas SAREF is in RDF/XML format.

```
import org.apache.jena.query.*;
import org.apache.jena.rdf.model.*;
import java.io.*;
import java.util.*;
import org.apache.jena.update.*;

public void addFileModel(File rdf, String riot) throws IOException {
    // parse the ontology file
    Model newModel = ModelFactory.createDefaultModel();
    try (FileInputStream in = new FileInputStream(rdf)) {
        newModel.read(in, null, riot);
    }
    
    DatasetAccessor accessor = DatasetAccessorFactory.createHTTP(“http://localhost:3030/energyds”);
    // Add statements to the default model of a Dataset
    accessor.add(newModel);      
}

public void addUrlModel (String urlString, String riot) throws Exception {
     // parse the ontology file
     Model newModel = ModelFactory.createDefaultModel();
        
     // create the url
     URL url = new URL(urlString);
     newModel.read(url.openStream(), null, riot);
     
     DatasetAccessor accessor = DatasetAccessorFactory.createHTTP(“http://localhost:3030/energyds”);
     // Add statements to the default model of a Dataset
     accessor.add(newModel);       
}

public void loadEnergyExample () {
    String sarefOntology ="http://ontology.tno.nl/saref.owl";
    String saref4EnerOntology ="http://ontology.tno.nl/saref4ener.ttl";
    String example ="example.ttl";
    try {
        addUrlModel(sarefOntology, "RDF/XML");
        addUrlModel(saref4EnerOntology, "TURTLE");
        addFileModel(new File(example), "TURTLE");
    } catch (Exception ex) {
        System.err.println (ex.getMessage());
    }
}        
```

In order to retrieve the values of the measurements of the heating system from the energy use case we need to make a SPARQL query. The method getMeasurements written below will print the properties, values and units of the measurements from the PowerProfile-1-HS0001 instance. The method queryModel contains the code to query the dataset providing as input a string with a query in SPARQL syntax.
```
public List<Map<String, Object>> queryModel(String sparqlQuery) {
    List<Map<String, Object>> mapResult = new ArrayList<>();

    try (QueryExecution qexec = QueryExecutionFactory.sparqlService(“http://localhost:3030/energyds”, sparqlQuery)) {
        org.apache.jena.query.ResultSet results;
        results = qexec.execSelect();

        while (results.hasNext()) {
            QuerySolution soln = results.nextSolution();
            mapResult.add(createMap(soln));
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

public void getMeasurements () {
    List<Map<String, Object>> qryResult;
    String sparqlQuery = "PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> "
                + "PREFIX s4ener: <https://w3id.org/saref4ener#> "
                + "PREFIX saref: <https://w3id.org/saref#> "
                + "SELECT ?x ?y ?m ?a ?b "
                + "WHERE {"
                + " ?x rdf:type s4ener:PowerProfile . " 
                + " ?x s4ener:belongsTo s4ener:HeatingSystem . " 
                + " ?x saref:isAbout ?y . " 
                + " ?m saref:relatesToProperty ?y . "
                + " ?m saref:hasValue ?a . " 
                + " ?m saref:isMeasuredIn ?b ."
                + " } ";

    qryResult = queryModel(sparqlQuery);

    int i = 0;
    while (i < qryResult.size()) {
        Resource resMeasurement = (Resource) qryResult.get(i).get("x");
        
        System.out.println (resMeasurement.getURI());
        System.out.println ("Property " + ((Resource)qryResult.get(i).get("y")).getLocalName());
        System.out.println ("Value " + qryResult.get(i).get("a"));
        System.out.println ("Unit " + ((Resource)qryResult.get(i).get("b")).getLocalName());
        i++;
    }
}
```

The output of invoking the method getMeasurements with the instances in the file [example.ttl](https://github.com/martin-p-bauer/2018_JWP/blob/master/part2/example.ttl) are shown below.

```
https://w3id.org/saref4ener#PowerProfile-1-HS0001
Property Power_1
Value 0.2
Unit kilowatt
https://w3id.org/saref4ener#PowerProfile-1-HS0001
Property Energy_1
Value 0.2
Unit kilowatt_hour
```

## Code implementation with OLGA 

OLGA example: https://github.com/EcoStruxure/OLGA/wiki/Hello-World

