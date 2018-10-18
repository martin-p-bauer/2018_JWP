# Retrieving Semantic Information [Martin Bauer]

___
_Once you have created instances of semantic information or annotated information, you want to make this information available to applications in a suitable and efficient way. For accessing semantic information, query languages and APIs have been defined. In our smart home energy use case, relevant information is about devices, their state, measurements and energy profiles._
___

As shown in the previous sections, semantic information is typically encoded as RDF triples (subject, predicate, object) in different representations. Objects in one triple can be subjects in other triples, so taking all triples together, we get an information graph. An example is shown below.

![RDF information graph example](https://github.com/martin-p-bauer/2018_JWP/blob/master/img/SarefRoomGraph.jpg)
 
SPARQL (SPARQL Protocol and RDF Query Language) [1] is the most commonly used query language to query such an information graph consisting of RDF triples. It provides a set of query functionalities, i.e. join, sort and aggregate, together with graph traversal syntax, e.g. as shown below:

*	What devices are associated with Room1001?
```
	PREFIX saref4ener: <https://w3id.org/saref4ener>
	PREFIX rooms: <https://myrooms.org>
	SELECT ?device
	WHERE
	  {
		rooms:Room1001  saref4ener:hasDevice	 ?device
	  }
```
The result is a set of matching assignments, i.e.
```
	device
	<https://mydevices.org/ts001>
	<https://mydevices.org/wm002>
```

*	What is the temperature in Room1001?
```
	PREFIX saref: <https://w3id.org/saref>
	PREFIX saref4ener: <https://w3id.org/saref4ener>
	PREFIX rooms: <https://myrooms.org>

	SELECT ?temperature
	WHERE
	  {
		Rooms:Room1001 saref4ener:hasDevice	 ?device
		?device   	rdf:type	 saref:TemperatureSensor
              	?device   	saref:hasValue	 ?temperature
	  }
```
The result is the following match:
```
	temperature
	25
```

As shown in the second example, SPARQL enables joins across triples. This works well in centralized architectures – i.e. where all information is available locally – and can be extended to distributed architectures, in which distribution is limited or it is known where to find what triples. However, such expressiveness is problematic in highly distributed settings, where relevant triples could be found anywhere. 

An API that targets semantic context information is NGSI-LD [2]. The underlying information model is based on entities, which have a semantic type. Entities have properties used to describe aspects of the respective entity and relationships to other entities. Thus the resulting model represents an entity graph. Properties and relationships can again be further described with another level of properties and relationships. Overall, the NGSI-LD information model is less general, but provides a higher abstraction level.  
It is based on JSON-LD, which is a representation of RDF – see example representation for Room1001. 

![NGSI-LD information graph example](https://github.com/martin-p-bauer/2018_JWP/blob/master/img/NGSI-LD-RoomGraph.jpg)

```
{
 	"id": "urn:ngsi-ld:Room:1001",
  	"type": "Room",
 	"temperature": {
   		"type": "Property",
		"value": "25"
	},
 	"hasDevice": {
   		"type": "Relationship",
   		"object": "urn:ngsi-ld:TemperatureSensor:ts001",
   		"deployedAt": {
        	"type": "Property",
        	"value": "2018-10-18T16:40:20"
     	} 
 	},
	"@context": [
		"http://uri.etsi.org/ngsi-ld/coreContext.jsonld",
		"http://example.org/ngsi-ld/commonTerms.jsonld",
		"http://example.org/ngsi-ld/rooms.jsonld", 
		"http://example.org/ngsi-ld/devices.jsonld" 
	]
}
```

The NGSI-LD API enables synchronous queries for entities, as well as asynchronous subscribe-notify interactions relating to changes in the information. The requested entities, properties and relationships can be specified and filtering of results can be based on property values and relationship objects.
With requests based only on the entity type or existing properties/relationships, new entities can be discovered, e.g. the following query for the temperature of all Rooms where the temperature is larger than 20.

```
GET /ngsi-ld/entities/?type=Room&attrs=temperature&q=temperature>20
Accept: application/ld+json
Link: <http://example.org/cim/aggregatedContext.jsonld>; rel="http://www.w3.org/ns/json-ld#context"; type="application/ld+json"
```

As location is highly relevant in real-world related use cases, NGSI-LD enables the geographic scoping of request – which may also be necessary to make entity type based discovery practical, e.g. request all entities within 2000m of a geographic coordinate:

```
GET /ngsi ld/entities/?type=Vehicle&georel=near;maxDistance==2000 &geometry=Point&coordinates=[8.684783577919006, 49.406131991436396]
Accept: application/ld+json
Link: <http://example.org/cim/aggregatedContext.jsonld>; rel="http://www.w3.org/ns/json-ld#context"; type="application/ld+json"
```

In order to support distributed and federated cases, information sources can register what kind of information they can provide on request with brokers or associated registries. Applications then only need to query a single Broker, which can find the information based on the registration and retrieve it on behalf of the application.
The NGSI-LD API is more specific than SPARQL, on a higher abstraction level (entity model) and overall less expressive, but as a result can better handle highly distributed and federated cases. As the NGSI-LD information is based on JSON-LD and thus RDF, it is possible to first retrieve relevant parts of the entity graph with a couple of requests. Then the results can be put together, resulting in an RDF graph, on which SPARQL queries with their full expressiveness can be executed locally.

[1] SPARQL 1.1 Overview, W3C Recommendation 21 March 2013, http://www.w3.org/TR/sparql11-overview/

[2] NGSI-LD Draft, ETSI Group Specification CIM 004, ETSI Industry Specification Group for cross-cutting Context Information Management (ETSI ISG CIM) , https://www.etsi.org/deliver/etsi_gs/CIM/001_099/004/01.01.01_60/gs_CIM004v010101p.pdf
 

