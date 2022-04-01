---
layout: base
title: Generating Patient Pathways using a Simulation Approach - SynPath
permalink: SynPath.html
---

<h2> {{page.title}} </h2>

Patient pathways are extremely rich data sources with information on detailed timings on healthcare activities and outcomes.   These data could be used to understand the impact of a specific intervention on a patient's health or to identify the effect of comorbidities on treatment options.  They are also excellent visualisations of a patient's journey and experience.  

However these data are also very sensitive as the timing component of activities makes the data very disclosive for any individual.  Therefore, sharing and collating these pathways into sources which can be accessed by researchers and innovators is extremely problematic.  

Synthetic data is one option to at least give a source of useable realistic pathways without breaking privacy.  Whilst these pathways would never be used for evidence based decisions or clinical insight, they would support the development of tools and techniques which could then be appropriately applied to the real data in a secure context.  Therefore, we wanted to investigate the creation and development of a pathways simulator - a tool which would be able to produce realistic but safe pathways. 

This piece is set out to talk through:
Our approach and other similar work
Our design of a standard but flexible reusable tool
Specific development of the patient module, service points and learning algorithms

## Our Approach and other Similar Work

Simulators allow for data to be created from scratch.  This means no privacy issues as we aren’t using any individuals data, but it also means lower quality as we have to rely on a set of rules for how any individual pathway can be generated.  This often leads to the simulators either generating data with low variability or only being able to focus upon a very specific set of pathways which can be well defined collectively.  

A few really good simulators are already out there including:
- [google/simhospital](https://github.com/google/simhospital) 
- [smart-on-fhir/sample-patients](https://github.com/smart-on-fhir/sample-patients)
- [synthetichealth/synthea](https://synthea.mitre.org/) - A java-based synthetic patient generator that models the medical history of synthetic patients.  The project’s mission is to output high-quality synthetic, realistic but not real, patient data and associated health records covering every aspect of healthcare. The resulting data is free from cost, privacy, and security restrictions.  See their [wiki](https://github.com/synthetichealth/synthea/wiki) for information on the supported diseases (e.g. Asthma) and formats (e.g. HL7 FHIR).  See ARTICLE to see our intention to develop Synthea for usage within NHS England. 
- [Hash.ai](https://hash.ai/) - an online platform for developing agent based models

## Our design of a standard but flexible reusable tool

When developing our simulator we wanted to create something that could be used as a foundation for more specific models to be built on.  This would then allow flexibility for the end use-case whilst ensuring models could be benchmarked and compared.   The simulator is built in different modules along the same lines as an agent based model:
- The patient data model (Data)
- The service points (Environment)
- Learning (Intelligence)

The patient data module and service points are designed to be extensible but wouldn’t allow a large amount of change.   The Learning could be completely re-written and applied in different ways to allow for flexibility.  

To make the outputs useable for innovators we wanted to ensure the outputs were both readable to the developer and also outputted in industry standard formats.  Therefore we have created the framework to outpt FHIR bundles

## Specific development of the patient module, service points and learning algorithms

The initial piece of development work focussed on the data model (“Patient Agent”).   This data model includes a series of properties to make the patient identifiable in the simulation including patient_id, gender, and birth_date.    Additionally, the patient is assigned a health record (conditions, medications, ..) and the ability for other attributes to be formally defined or set through keyword arguments (kwargs).    The data model then allows three methods to be applied ot the patient agent which are update, save and load.  

The environment represents a physical location (e.g. GP practice) or a more abstract entity (e.g. multidisciplinary team meeting).  The environment interacts with the patient agent’s record and results in an update to that record.   These environment objects have been designed to not be overly specified in attributes and methods so that they can be generalised and allow the creation of more specific environments subclassed in the future.   


# Contact

Please get in contact through analytics-unit@nhsx.nhs.uk if you would like to discuss this specific project or to discuss the generation of synthetic data in general.  
