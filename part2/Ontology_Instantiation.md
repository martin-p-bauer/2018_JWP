# Ontology Instantiation [Charbel Kaed]
Given an ontology, how can this ontology be instantiated for a concrete use case.

Example of ontology instantiation for the use case on energy efficiency. 

It shows an example of how to instantiate a power profile using the SAREF4ENER extension of SAREF. This power profile is used by an heating system with hot water tank to communicate its energy flexibility to the CEM according to the consumer's preferences and needs. The corresponding Turtle code is provided below. A distinction between SAREF and SAREF4EE is made using the prefixes saref: and s4ener:, respectively.

A s4ener:PowerProfile inherits the properties of the more general saref:Profile, extending it with additional properties that are specific for SAREF4ENER. The s4ener:PowerProfile is used by a s4ener:Device to expose the power sequences that are potentially relevant for the CEM, for example, a heating system with hot water tank that wants to communicate its expected energy consumption for a certain day (s4ener:HeatingSystem instance). The s4ener:HeatingSystem exposes a s4ener:PowerProfile (s4ener:PowerProfile-1-HS0001 instance), which consists of two groups with alternative plans (each group is modelled as a s4ener:AlternativesGroup class). These groups do not overlap in time and allow to model consecutive (and also rather independent) periods of action. For example, the s4ener:PowerProfile-1-HS0001 contains one group of alternatives for a task in the morning, and another group of alternatives for another (additional) task in the afternoon. Within one group, there can be one or more plans represented by s4ener:PowerSequence classes (i.e. s4ener:AlternativesGroup-1-HS0001 and s4ener:AlternativesGroup-2-HS0001) which are alternatives to each other (i.e. at most one of these plans can be finally executed). For example, to charge the hot water tank, the heating system mentioned above can offer within the "afternoon alternative group" two alternative plans, represented as power sequences: (a) a "cheapest" plan in which the CEM should try to minimize the user's energy bill, and (b) a "greenest" plan in which the CEM should try to optimize the configuration towards the maximum availability of renewable energy. 

Therefore, in the afternoon group (s4ener:AlternativesGroup-2-HS0001) the heating system offers two different power sequences: (a) s4ener:PowerSequence-3-HS0001 that aims to run "as cheap as possible" and permits the CEM to shift the start between 8:45 and 12:00, and (b) s4ener:PowerSequence-2-HS0001 that aims to reduce energy (it can even announce the user's preference for "green energy"). This means for the afternoon the CEM can take a choice for the "cheap" or the "green" plan. The plans may have further options with regards to their flexibility. For example one of the plans may offer that the CEM can pause a sequence (as long as the sequence completes before the latest time set by the user). Finally, a s4ener:PowerSequence consists of one or more slots (s4ener:Slot class) that represent different phases of consumption (or production) and their values. The power sequences of the heating system example have a single slot each. However, for other devices such as washing machines, a power sequence may have various slots for the different phases of washing, such as heating the water, washing and rinsing.

RDF code for SAREF4ENER example
# baseURI: http://ontology.tno.nl/examples/saref4ener/heatingsystem
# imports: https://w3id.org/saref4ener

@prefix heatingsystem: <http://ontology.tno.nl/examples/saref4ener/heatingsystem#> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix s4ener: <https://w3id.org/saref4ener#> .
@prefix saref: <https://w3id.org/saref#> .
@prefix time: <http://www.w3.org/2006/time#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<http://ontology.tno.nl/examples/saref4ener/heatingsystem>
  rdf:type owl:Ontology ;
  owl:imports <https://w3id.org/saref4ener> ;
  .
time:Beginning_PowerProfile-1-HS0001
  rdf:type time:Instant ;
  rdfs:label "Beginning Power profile-1-HS0001"^^xsd:string ;
  time:inXSDDateTime "2016-12-15T00:01:01.01"^^xsd:dateTime ;
.
time:Beginning_PowerSequence-HS0001_afternoon
  rdf:type time:Instant ;
  rdfs:label "Beginning Power sequence-HS0001 afternoon"^^xsd:string ;
  time:inXSDDateTime "2016-12-15T15:30:00.00"^^xsd:dateTime ;
.
time:Beginning_PowerSequence-HS0001_morning
  rdf:type time:Instant ;
  rdfs:label "Beginning Power sequence-HS0001 morning"^^xsd:string ;
  time:inXSDDateTime "2016-12-15T08:45:00.00"^^xsd:dateTime ;
.
time:DateTimeInterval_PowerProfile-1-HS0001
  rdf:type time:DateTimeInterval ;
  rdfs:label "Date time interval Power profile-1-HS0001"^^xsd:string ;
  time:hasBeginning time:Beginning_PowerProfile-1-HS0001 ;
  time:hasEnd time:End_PowerProfile-1-HS0001 ;
.
time:End_PowerProfile-1-HS0001
  rdf:type time:Instant ;
  rdfs:label "End Power profile-1-HS0001"^^xsd:string ;
  time:inXSDDateTime "2016-12-15T00:23:59.59"^^xsd:dateTime ;
.
time:End_PowerSequence-HS0001_afternoon
  rdf:type time:Instant ;
  rdfs:label "End Power sequence-HS0001 afternoon"^^xsd:string ;
  time:inXSDDateTime "2016-12-15T00:18:00.00"^^xsd:dateTime ;
.
time:End_PowerSequence-HS0001_morning
  rdf:type time:Instant ;
  rdfs:label "End Power sequence-HS0001 morning"^^xsd:string ;
  time:inXSDDateTime "2016-12-15T00:12:00.00"^^xsd:dateTime ;
.
time:PowerSequence-HS0001_afternoon
  rdf:type time:DateTimeInterval ;
  rdfs:label "Power sequence-HS0001 afternoon"^^xsd:string ;
  time:hasBeginning time:Beginning_PowerSequence-HS0001_afternoon ;
  time:hasEnd time:End_PowerSequence-HS0001_afternoon ;
.
time:PowerSequence-HS0001_morning
  rdf:type time:DateTimeInterval ;
  rdfs:label "Power sequence-HS0001 morning"^^xsd:string ;
  time:hasBeginning time:Beginning_PowerSequence-HS0001_morning ;
  time:hasEnd time:End_PowerSequence-HS0001_morning ;
.
s4ener:AlternativesGroup-1-HS0001
  rdf:type s4ener:AlternativesGroup ;
  rdfs:label "Alternatives group-1-HS0001"^^xsd:string ;
  saref:consistsOf s4ener:PowerSequence-1-HS0001 ;
  s4ener:alternativesGroupID 1 ;
  s4ener:belongsTo s4ener:PowerProfile-1-HS0001 ;
.
s4ener:AlternativesGroup-2-HS0001
  rdf:type s4ener:AlternativesGroup ;
  rdfs:label "Alternatives group-2-HS0001"^^xsd:string ;
  saref:consistsOf s4ener:PowerSequence-2-HS0001 ;
  saref:consistsOf s4ener:PowerSequence-3-HS0001 ;
  s4ener:alternativesGroupID 2 ;
  s4ener:belongsTo s4ener:PowerProfile-1-HS0001 ;
.
s4ener:EndTimeDurationDescription_PS-1-HS0001
  rdf:type s4ener:EndTimeDurationDescription ;
  rdfs:label "End time duration description PS-1-HS0001"^^xsd:string ;
.
s4ener:EndTime_PS-1-HS0001
  rdf:type s4ener:EndTime ;
  rdfs:label "End time PS-1-HS0001"^^xsd:string ;
.
s4ener:Energy_1
  rdf:type s4ener:Energy ;
  rdfs:label "Energy 1"^^xsd:string ;
  saref:isMeasuredByDevice s4ener:HeatingSystem ;
.
s4ener:Heating
  rdf:type saref:Task ;
  rdfs:label "Heating"^^xsd:string ;
.
s4ener:HeatingSystem
  rdf:type s4ener:Device ;
  rdfs:label "Heating system"^^xsd:string ;
  saref:accomplishes saref:EnergyEfficiency ;
  saref:accomplishes s4ener:Heating ;
  saref:hasDescription "Heating system HS0001 is an example of how to instantiate a heating system with hot water tank using SAREF4ENER"^^xsd:string ;
.
s4ener:Measurement_1
  rdf:type saref:Measurement ;
  rdfs:label "Measurement 1"^^xsd:string ;
  saref:hasValue "0.2"^^xsd:string ;
  saref:isMeasuredIn <http://www.wurvoc.org/vocabularies/om-1.8/kilowatt_hour> ;
  saref:relatesToProperty s4ener:Energy_1 ;
.
s4ener:Measurement_2
  rdf:type saref:Measurement ;
  rdfs:label "Measurement 2"^^xsd:string ;
  saref:hasValue "0.2"^^xsd:string ;
  saref:isMeasuredIn <http://www.wurvoc.org/vocabularies/om-1.8/kilowatt> ;
  saref:relatesToProperty s4ener:Power_1 ;
.
s4ener:PowerProfile-1-HS0001
  rdf:type s4ener:PowerProfile ;
  rdfs:label "Power profile-1-HS0001"^^xsd:string ;
  saref:consistsOf s4ener:AlternativesGroup-1-HS0001 ;
  saref:consistsOf s4ener:AlternativesGroup-2-HS0001 ;
  saref:hasTime s4ener:Time_PowerProfile-1-HS0001 ;
  saref:isAbout s4ener:Energy_1 ;
  saref:isAbout s4ener:Power_1 ;
  s4ener:alternativesCount 2 ;
  s4ener:belongsTo s4ener:HeatingSystem ;
  s4ener:nodeRemoteControllable "true"^^xsd:boolean ;
  s4ener:supportsReselection "true"^^xsd:boolean ;
  s4ener:supportsSingleSlotSchedulingOnly "true"^^xsd:boolean ;
  s4ener:totalSequencesCountMax "1"^^xsd:unsignedInt ;
.
s4ener:PowerSequence-1-HS0001
  rdf:type s4ener:PowerSequence ;
  rdfs:label "Power sequence-1-HS0001"^^xsd:string ;
  saref:consistsOf s4ener:Slot-1-HS0001 ;
  saref:hasTime time:PowerSequence-HS0001_morning ;
  saref:hasTime s4ener:StartTime_1 ;
  s4ener:belongsTo s4ener:AlternativesGroup-1-HS0001 ;
  s4ener:isPausable "false"^^xsd:boolean ;
  s4ener:isStoppable "false"^^xsd:boolean ;
.
s4ener:PowerSequence-2-HS0001
  rdf:type s4ener:PowerSequence ;
  rdfs:label "Power sequence-2-HS0001"^^xsd:string ;
  saref:consistsOf s4ener:Slot-2-HS0001 ;
  saref:hasTime time:PowerSequence-HS0001_afternoon ;
  saref:hasTime s4ener:StartTime_1 ;
  s4ener:belongsTo s4ener:AlternativesGroup-2-HS0001 ;
  s4ener:greenest "true"^^xsd:boolean ;
  s4ener:isPausable "false"^^xsd:boolean ;
  s4ener:isStoppable "false"^^xsd:boolean ;
.
s4ener:PowerSequence-3-HS0001
  rdf:type s4ener:PowerSequence ;
  rdfs:label "Power sequence-3-HS0001"^^xsd:string ;
  saref:consistsOf s4ener:Slot-3-HS0001 ;
  saref:hasTime time:PowerSequence-HS0001_afternoon ;
  saref:hasTime s4ener:StartTime_1 ;
  s4ener:belongsTo s4ener:AlternativesGroup-2-HS0001 ;
  s4ener:cheapest "true"^^xsd:boolean ;
  s4ener:isPausable "false"^^xsd:boolean ;
  s4ener:isStoppable "false"^^xsd:boolean ;
.
s4ener:Power_1
  rdf:type s4ener:Power ;
  rdfs:label "Power 1"^^xsd:string ;
  saref:isMeasuredByDevice s4ener:HeatingSystem ;
  saref:relatesToMeasurement s4ener:Measurement_2 ;
.
s4ener:Slot-1-HS0001
  rdf:type s4ener:Slot ;
  rdfs:label "Slot 1 HS0001"^^xsd:string ;
  s4ener:belongsTo s4ener:PowerSequence-1-HS0001 ;
  s4ener:hasEnergyValueType s4ener:Energy_1 ;
  s4ener:hasPowerValueType s4ener:Power_1 ;
  s4ener:slotNumber "1"^^xsd:unsignedInt ;
.
s4ener:Slot-2-HS0001
  rdf:type s4ener:Slot ;
  rdfs:label "Slot 2 HS0001"^^xsd:string ;
  s4ener:belongsTo s4ener:PowerSequence-2-HS0001 ;
  s4ener:slotNumber "2"^^xsd:unsignedInt ;
.
s4ener:Slot-3-HS0001
  rdf:type s4ener:Slot ;
  rdfs:label "Slot 3 HS0001"^^xsd:string ;
  s4ener:belongsTo s4ener:PowerSequence-3-HS0001 ;
  s4ener:slotNumber "3"^^xsd:unsignedInt ;
.
s4ener:StartTimeDurationDescription_1
  rdf:type s4ener:StartTimeDurationDescription ;
  rdfs:label "Start time duration description 1"^^xsd:string ;
  s4ener:xsdDuration "PT0H5M"^^xsd:duration ;
.
s4ener:StartTime_1
  rdf:type s4ener:StartTime ;
  rdfs:label "Start time 1"^^xsd:string ;
  time:hasDurationDescription s4ener:StartTimeDurationDescription_1 ;
.
s4ener:Time_PowerProfile-1-HS0001
  rdf:type saref:Time ;
  rdfs:label "Time Power profile-1-HS0001"^^xsd:string ;
  saref:consistsOf time:DateTimeInterval_PowerProfile-1-HS0001 ;
.
