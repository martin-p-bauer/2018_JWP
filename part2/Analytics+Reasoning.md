# Analytics and Reasoning using Semantic Information [Amelie Gyrard, Laura Daniele, Martin Serrano]
How to do analytics and reasoning using semantic information.


Example of rule complaint with the Jena framework

[UnhealthyOutdoorAirQualityIndexUS: 
              (?measurement rdf:type kao:OutdoorAirQualityIndex)
              (?measurement sosa:hasSimpleResult ?v)
              greaterThan(?v,101)
              lessThan(?v,150)
			  ->
				(?measurement rdf:type kao:UnhealthyOutdoorAirQualityIndexUS)
]
According to Wikipedia Air Quality Index (AQI): https://en.wikipedia.org/wiki/Air_quality_index
Rule: IF AirQualityIndex greaterThan 101 and LowerThan 150 THEN UnhealthyOutdoorAirQualityIndexUS

References:
- Sensor-based Linked Open Rules (S-LOR): http://linkedopenreasoning.appspot.com/
 http://linkedopenreasoning.appspot.com/?p=publication
 - Sensor-based Linked Open Rules (S-LOR): An Automated Rule Discovery Approach for IoT Applications and its use in Smart Cities [Gyrard et al. Smart City Workshop WWW 2017]
 - Book Chapter: A Review of Tools for IoT Semantics and Data Streaming Analytics [Serrano, Gyrard et al. 2016]
 - Knowledge Extraction from Sensor Data, Knowledge Acquisition Tooolkit (KAT): http://info.ee.surrey.ac.uk/CCSR/KAT/overview.html
