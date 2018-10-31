# Part 1

# 1 Towards semantic interoperability standards that can be used in practice
Part 1 provides a rationale for the need to develop semantic interoperability standards according to a process taking into account industry needs. It identifies conditions under which this process, i.e. an interoperability-by-design best practice, can be applied by stakeholders in the industry to develop semantic interoperability standards.
## 1.1 Rationale for industry practice
The benefit of applying semantic interoperability processes in the industry will be the following:
* A systematic process is applied, which improves the quality of a specification
* The resulting specification can be used as a reference when interpretation problems have to be solved
* Most importantly, the maintenance and extension of an interoperability specification will be straightforward with a better guarantee that no regression is created.
## 1.2 Industry requirements for semantic interoperability standard development
In order to get successful standards on semantic interoperability specifications, a number of requirements must be taken in account by organisations that wish to build a standard:
* Co-creation and separation of concern
* Defining the knowledge perimeter needed for a specification
* Evaluation of a specification
* Support of industry deployment concerns
### Co-creation and separation of concern
The practice of semantic interoperability requires multiple expertise: domain experts bring knowledge on domain engineering, semantic interoperability experts bring knowledge on ontology engineering. Depending on the domain, other categories of experts might also be needed such as security and privacy exerts, or user-centric design experts.
It is however important to achieve a clear separation of concern between domain experts and semantic interoperability experts. Without this separation of concern, we can get into the trap that a domain expert has to rely on a semantic interoperability expert to propose a specification, and end up with decisions that are taken by the wrong expert. From a method and tools viewpoint, we believe that recommendations must be provided in approaches to create separation of concern. For instance, domain experts should be able to inspect and update a specification using a domain viewpoint, while the semantic interoperability experts should be able to focus on the semantic interoperability mechanics soundness.

|Example|Description|
|----|----|
| Example of practice integrating separation of concern | An example of good separation of concern is to have specific co-creation sessions when both categories are present to make design decision. This was achieved by the SAREF team when they organized a session for the European Large Scale Pilots during the IoT week in Bilbao in June 2018 to get input from domain experts that they could use in the specification of an ontology. |
### Defining the knowledge perimeter needed for a specification
It is important to clearly define the knowledge perimeter needed for a specification. An ontology could cover an entire domain (e.g. energy). This could be unnecessary and even counter effective if the need is to focus on a more restricted perimeter. This is particularly important when cross domain ontologies are defined, i.e. one does not have to access an entire domain ontology, but rather the subset that is useful to build a cross domain ontology.

|Example|Description|
|----|----|
| Example of practice for scope of specification | An interoperability specification is defined to allow for cross domain interoperability between an energy management system and electric vehicle charging system. The resulting ontology covers a common subset of the energy and mobility domain. |
### Evaluation of a specification
It is important to be able to evaluate the “usefulness” of a specification. One typical indicator is the level of consensus. A specification that has not reached consensus is likely not to be adopted. Semantic interoperability standards can fall into this trap if the domain experts get lost in the specification process. The goal should be that domain experts can constantly follow the specification process and agree on the content while semantic interoperability experts guarantee that the specification is sound.

|Example|Description|
|----|----|
| Example of practice for specification evaluation | Periodic evaluation of a specification is needed. It could rely on an indicator consisting of two TRL, a domain specification TRL which focuses on whether all domain needs are covered and an otology specification TRL, which focuses on whether the specification is well-formed. A specification is deemed mature of both TRL are high. Example of tools for assisting organisation could consist of associating TRL will parts of the specification. For instance this part is mature. This other part is the one that we are trying to improve. |
### Deployment concerns
It is important to be able to take into account deployment concerns in a specification of a semantic interoperability standard. At least two concerns should be taken into account:
* Provision for profiles and discovery. Some specifications might concern a market segment of a domain. For instance, high-end device manufacturers might want to add specific semantic specification concerning high-end features. Some specifications might even be proprietary. This can happen when device manufacturers agree that they will agree on co-existing solutions. This is often solved by service discovery capabilities. The concept of profiles should also be applied to semantic interoperability standards
* Support for version management. Semantic interoperability specifications will evolve as a domain evolves to match the needs of different generations of products (e.g., a new generation of smartphone) The rules for compatibility must be anticipated. For instance, we could have a SAREF v1 ontology for a domain that is then replaced by SAREF v2 ontology Rules [Amélie: not clear] for allowing this evolution must be agreed upfront.

|Example|Description|
|----|----|
| Example of practice for profiles | The concept of profiles is handled at the ontology level (either as part of the ontology, or as part of tools supporting the ontology). It is for instance possible to browse an ontology from a profile viewpoint. Some ontologies subsets could even be confidential, involving IPR. |
| Example of practice for version management | A washing machine uses SAREF v1 ontology. In a second generation of washing machine, an extended specification is needed to allow control of the washing machine by an AI agent. This requires an extension of the SAREF v1 ontology to a SAREF v2 ontology. All new generation washing machines are upward compatible with SAREF v1 ontology. |
## 1.2 System viewpoint to avoid fragmentation of semantic interoperability specifications
The table below describes a number of important initiatives on semantic interoperability. While it is important to foster such developments, there is a need for convergence in order to avoid the following risks:
* Risk of lack of interoperability caused by the use of incompatible specification languages. 
* Babel tower situation [amélie: i know a little bit about this, but not clear here] caused by the specification of incompatible semantics.
* Fragmentation [amélie: lack of interoperability? what is fragmentation] caused by incompatible system approaches. 
A system viewpoint should be taken as proposed by SAREF in Figure 1.


![](https://github.com/martin-p-bauer/2018_JWP/blob/master/Saref%20system%20vision.PNG)

<p align="center">
Figure 1 : Example of system vision
</p>



| Initiative | Description |
|----|----|
| W3C Semantic Sensor Networks | As depicted in the previous table, there is no common benchmark to evaluate all the triple-stores. However, the selection of a triple store will be fundamentally based on the type of inferencing you need in the project (RDF, RDFS, OWL), the type of the project (commercial or open source) and the initial information capacity expected for your application. Other key aspects to have in mind at time of selecting a semantic store is the performance capacity. That means, how the semantic store perform the inferences and where the information is stored. A big lack of the semantic stores is that they needs huge resources to perform the corresponding inferencing, process and load the information. This main lack is derived mainly by the mix of storing the information in different files and in-memory. | 
| W3C Web of Things | The Web of Things (WoT) is an extension of the Internet of Things (IoT) to ease the access to data using the benefits of Web technologies [2]. Data is generated by things/devices and then exploited by more and more web-based applications to monitor healthcare or even control home automation devices. The W3C Web of Things (WoT) Interest Group is designing a vocabulary to describe interactions between objects through the Web, a potential implementation is the WoT ontology [4]. At the current date of writing, WoT ontology is not aligned with W3C SSN ontologies. A healthcare scenario has been designed "Remote health monitoring system" [5] among several use cases. |
| OneM2M | OneM2M, an international standard for Machine-to-Machine (M2M) with the development of the OneM2M ontology [6]. It extends the European ETSI M2M standard. At the current date of writing, OneM2M is not aligned with W3C SSN. | 
| MyOntoSens | MyOntoSens modular ontology, mainly based on SSN V1 and OGC standards, has been proposed in [Nachabe et al. 2015] as an improvement of existing WSNs ontologies. It has been standardized in 2015 for medical devices and BANs (Body Area Networks) as a Technical Specification (TS) within the SmartBAN Technical Committee of the ETSI standardization body [7]. This ontology is in particular relevant to build health, wellbeing/wellness and personal safety applications based on smart devices.| 
| SAREF| Smart Appliances REFerence (SAREF) [8], is a European standard supported by ETSI M2M and SmartM2M. It mainly covers the smart building applicative domain. The SAREF ontology has been designed re-using SSN and oneM2M according to [Moreira et al. 2017]. Schema.org. Schema.org is a well-known schema catalog to structure data on Web pages to describe the location, person, etc. The IoT Schema.org extension [9] is planned; discussions are ongoing. | 
| Haystack | Haystack [10] is a project aiming at standardizing semantic data models and web services. For instance, the Haystack Tagging Ontology which employs SSN V1 ontology has been developed [11] [Charpenay et al. 2015].| 

## 1.3 Interoperability-by-design: a lifecycle description
The following phases are defined:

(1) Stakeholder needs and requirements. This includes

-	the description of the domain and the system;
- the description of the interoperability point;
- the description of the needed knowledge and the needed expertise; and
- the description of industry deployment requirements.

(2) Semantic interoperability requirements definition

(3) Semantic interoperability ontology structure co-creation

(4) Semantic interoperability ontology co-construction

(5) Semantic interoperability ontology test and validation

(6) Semantic interoperability ontology commissioning and deployment

(7) Semantic interoperability ontology decommissioning 

### Example
To be provided. This section could provide an example on Ambient Assisted Living (AAL). It would demonstrate a use case combining 2 domains: smart homes and healthcare applications domains. AAL helps elderly people to stay independent at home.

## 1.4 Standardisation Roadmap proposal
To be provided. Drawing from the recommendations, this section could provide a proposed roadmap.

# Additional text from previous contributors
 
  ## Add Appendix section - with technical details for developers?
  an annexe/appendix section with all technical details would satisfy the developers? and the other audience won't be lost within the document
  
  Part 2 is now referencing a set of concrete tools for ontologies.
  
  ## Derive recommendations for semantic interoperability - "Lessons Learned, Recommendations and Best Practices" 
  we can add one section "Lessons Learned, Recommendations and Best Practices" at the end of the document
  - focus on semantic models (e.g., ontologies)
  - other ideas
  - best practices checklist summary 
  
   Check section Ontology Best Practices - Checklist Summary (page 11)
   
   http://perfectsemanticweb.appspot.com/documentation/SemanticWebBestPracticesForDummies.pdf 
  
