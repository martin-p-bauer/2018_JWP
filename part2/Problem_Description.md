# Problem Description [Michelle Wetterwald]

Several studies have demonstrated the fragmentation of the IoT eco-system in terms of standardization, available technologies and M2M service platforms. Accordingly, measurements and data available in one system or implementation is often not accessible to a different system. Furthermore, these systems are often still strongly dependent of the vertical domain in which they are implemented. 

Interoperability has been considered at various levels: technical (connectivity, network, syntactic), informational (semantic or business context) or even organizational. Technical levels cannot be easily achieved when addressing integrated platforms. The semantic or data level is thus the next level where interoperability can be envisioned. Furthermore, the different systems must share the same vocabulary and understand in an identical manner the information they exchange, while facilitating the design of service compositions. 

At this level, semantics can bring a valuable solution, since it defines a common and abstracted sub-layer above the services and platforms definition. Semantics interoperability thus enable the sharing of data across systems, avoiding the definition of a new common data model every time that two different systems need to exchange information.

As already aforementioned, one of the first interoperability level to take care of is at informational level, i.e. at data and semantic level. It is mandatory to address since it allows data heterogeneity management, both within a single platform and even across platform (provided that the data model become a unified / standardized one). One good example of that is the Bluetooth LE GATT (Generic Attributes) profile that has been standardized by the Bluetooth SIG and enables Bluetooth devices interoperability [https://www.bluetooth.com/specifications/gatt].


Figure 1: Simple example of a house room

Let us now take a simple example of a house room with a black box on a wall (see figure 1), e.g. a sensor that is providing the following instant value: 22°. A visitor of the house has as much power of reasoning as humams do and is therefore guessing (due to the position of the black box, the value provided on the black Box screen  ̶  22°  ̶ , his central European location) that the provided value is a temperature expressed in degree Celcius. A machine (e.g. a Device, an automated process, an application…) for its part is not able to do a lot with this instant value (22°) since it does not know how to analyze this raw data, mainly:

•	the meaning of the data, called metadata, e.g. in our home example a temperature measurement, with “Temperature” as name, ‘t’ as acronym, “°C” as unit of measure, “float” as measurement domain and 20 as value. With this metadata knowledge, few simple data analytics can already be performed, like e.g. in our home example, verifying if a  Temperature ‘t’ is not higher than 26,

•	and the context of the data, extending the metadata and called ontology, like e.g. in our home example, the information of the sensor that provides the data, the associated positioning and geolocalization, environment, room and home ID, home owner information. With that extended semantic knowledge, more powerful semantic data analytics can now be performed, like e.g. in our home example, which are the collocated houses that have the same Temperature value. 

Ontology design (i.e. specification, formalization) and implementation are thus mandatory for data heterogeneity management and semantic interoperability. It facilitates data/information sharing across systems and enables semantic-based embedded data analytics (e.g. for automated alarm management or control operations). If the ontology incorporates common upper level semantics, like e.g. service definition, then it enables data sharing at application level and also facilitates cross-domain use cases handling.  

The specification of a data model and its associated metadata/ontology is realized through the use of a modeling/representation tool, like the commonly used UML model, that allows the expression of the corresponding concepts and their relations. The formalization of the data model (onto the corresponding metadata/ontology) is realized through the use of a description language that is generally XML-based (e.g. OWL or RDF), except within embedded devices where lighter non-XML language like e.g. JSON or CBOR are preferred.
In the context of our room and temperature sensor example, and if we use the SAREF ontology, our temperature sensor can be viewed as a Device (saref:Device):

•	With saref:Sensor as device category,

•	That is provided with e.g. a Description (String), a Manufacturer (String), a model (String), a State (e.g. on or off) as properties,

•	That offers/performs sensing expressed as saref:Function, with saref:SensingFunction (which has a range, a sensing time and the sensor type  ̶  ‘Temperature’ in our example  ̶  as properties) as category, saref:GetCommand as command (i.e. GetTemperature in our example),

•	and that is used for sensing a temperature of type saref:Temperature. This ‘Temperature’ property (a saref:Property) has a unit of measure of the type saref:UnitOfMeasure (°C in our example), and has a Value (22 in our example).
This is summarized in Figure 2.

Figure2: Simple example of a house room – simplified SAREF representation of the temperature sensor
