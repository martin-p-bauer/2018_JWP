# Semantic Information / Semantic Annotation [Wenbin Li]

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

