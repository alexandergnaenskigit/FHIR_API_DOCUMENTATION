---
title: 'Clinical Data API'
---

The list below shows the main resources that were used by the FHIR Adapter.

- [Goal](https://hsfhirdocs.github.io/api_docs/profiles/Goal/US-Core.html)
- [Medication](https://hsfhirdocs.github.io/api_docs/profiles/Medication/basic.html)
- [Care Plan](https://hsfhirdocs.github.io/api_docs/profiles/CarePlan/US-Core.html)
- [Allergy Intolerance](http://hl7.org/fhir/us/core/StructureDefinition/us-core-allergyintolerance)
- [Condition](https://hsfhirdocs.github.io/api_docs/profiles/Condition/US-Core.html)
- [Patient](https://hsfhirdocs.github.io/api_docs/profiles/Patient/basic.html)
- Related Person
- [Procedure](https://hsfhirdocs.github.io/api_docs/profiles/Procedure/US-Core.html)
- User

<b>*Permissions are required to get access to this api</b>

## Queries examples:

### Patient

To get a list of patients, you can run the following query:

GET [base url]/Patient

To read a particular record use the following request:

GET [base url]/[resource name]/[id]

Where

[base url] - the base url (see above)

[resource name] - is the name of a resource you want to read

[id] - is a FHIR identifier

For example, to get data for a particular Practitioner you can run:

GET [base url]/Practitioner/4ec99942-c667-4d54-af23-f89f0792e4ed

You can get, for example, the following result:

{
    "meta": {
        "lastUpdated": "2021-06-11T19:38:39.686496Z",
        "createdAt": "2021-06-11T19:38:39.686496Z",
        "versionId": "11293018"
    },
    "name": [
        {
            "use": "official",
            "given": [
                "Sample",
                "A"
            ],
            "family": "Practitioner"
        }
    ],
    "birthDate": "1984-12-08"
    "resourceType": "Practitioner",
    "active": true,
    "id": "4ec99942-c667-4d54-af23-f89f0792e4ed",
    "identifier": [
        {
            "use": "secondary",
            "type": {
                "coding": [
                    {
                        "code": "externalId",
                        "display": "externalId",
                        "userSelected": false
                    }
                ]
            },
            "value": "89687",
            "system": "http://hl7.org/fhir/sid/external-id"
        },
        {
            "use": "official",
            "type": {
                "coding": [
                    {
                        "code": "NPI",
                        "display": "NPI",
                        "userSelected": false
                    }
                ]
            },
            "value": "1111111111",
            "system": "http://hl7.org/fhir/sid/us-npi"
        }
    ],
    "gender": "male"
}


### Procedure

[https://portal.aidbox.myparamount.org/fhir/Procedure?identifier=AD6DFBBEBE01C94E4268D6709963545A5168131623ADC065124BC3B27941B6C2](https://portal.aidbox.myparamount.org/fhir/Procedure?identifier=AD6DFBBEBE01C94E4268D6709963545A5168131623ADC065124BC3B27941B6C2)


More samples and additional information can be found here:

https://docs.aidbox.app/api-1/api/crud-1/read