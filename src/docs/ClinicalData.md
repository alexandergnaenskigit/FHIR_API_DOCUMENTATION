---
title: '3. Clinical Data API'
---
# Clinical Data API

Clinical Data API follows [US Core Implementation Guide](http://build.fhir.org/ig/HL7/US-Core/index.html)

The US Core Implementation Guide is based on FHIR Version R4 and defines the minimum set of constraints on the FHIR resources to create the US Core Profiles. It also defines the minimum set of FHIR RESTful interactions for each of the US Core Profiles to access patient data.

The list below shows the main resources that are used by the API.

- [Goal](../../profiles/Goal/US-Core.html)
- [Medication](../../profiles/Medication/basic.html)
- [Care Plan](../../profiles/CarePlan/US-Core.html)
- [Allergy Intolerance](http://hl7.org/fhir/us/core/StructureDefinition/us-core-allergyintolerance)
- [Condition](../../profiles/Condition/US-Core.html)
- [Patient](../../profiles/Patient/basic.html)
- [Procedure](../../profiles/Procedure/US-Core.html)

<b>*Permissions are required to get access to this api</b>

## Queries examples:

### Patient

To get a list of patients, you can run the following query:

GET [base url]/Patient


### Procedure

[https://portal.aidbox.myparamount.org/fhir/Procedure?identifier=AD6DFBBEBE01C94E4268D6709963545A5168131623ADC065124BC3B27941B6C2](https://portal.aidbox.myparamount.org/fhir/Procedure?identifier=AD6DFBBEBE01C94E4268D6709963545A5168131623ADC065124BC3B27941B6C2)


