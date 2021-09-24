---
title: '2. Provider Dirrectory Api'
---

This page contains short descriptions of Practitioner, PractitionerRole, Organization, and OrganizationAffiliation search queries, lists of search parameters, and sample queries.

# Provider Directory

- [Organization](https://hsfhirdocs.github.io/api_docs/profiles/Organization/DaVinci-PDEX-Plan-Net.html)
- [Practitioner](https://hsfhirdocs.github.io/api_docs/profiles/Practitioner/DaVinci-PDEX-Plan-Net.html)
- [Location](https://hsfhirdocs.github.io/api_docs/profiles/Location/DaVinci-PDEX-Plan-Net.html)
- [Healthcare Service](https://hsfhirdocs.github.io/api_docs/profiles/HealthcareService/DaVinci-PDEX-Plan-Net.html)
- [Organization Affiliation](https://hsfhirdocs.github.io/api_docs/profiles/OrganizationAffiliation/DaVinci-PDEX-Plan-Net.html)
- [Practitioner Role](https://hsfhirdocs.github.io/api_docs/profiles/PractitionerRole/DaVinci-PDEX-Plan-Net.html)
- [Insurance Plan](https://hsfhirdocs.github.io/api_docs/profiles/InsurancePlan/DaVinci-PDEX-Plan-Net.html)


We store information about practitioners in these FHIR Entities:

- Practitioner - basic info about а practitioner. Contains demographics, specialty, language and identifiers like NPI and IRS
- PractitionerRole - central entity to connect practitioner's entities. Also contains info about available time
- Organization - practitioner's place of work
- Network - info about health plans a practitioner is connected with
- Location - practitioner's location info (address) and telecom info (phone, email) 
- HealthcareService - services provided by a practitioner

## Sample Queries

Practitioner queries examples:

- Get 100 practitioners (by default)<br/>
  [https://portal.aidbox.myparamount.org/fhir/Practitioner](https://portal.aidbox.myparamount.org/fhir/Practitioner)
- Get practitioner by name<br/>
  [https://portal.aidbox.myparamount.org/fhir/Practitioner?name=Garner%20Melanie](https://portal.aidbox.myparamount.org/fhir/Practitioner?name=Garner%20Melanie)
- Get practitioner by identifier<br/>
  [https://portal.aidbox.myparamount.org/fhir/Practitioner?identifier=22240](https://portal.aidbox.myparamount.org/fhir/Practitioner?identifier=22240)


### PractitionerRole

PractitionerRole is a central entity for a practitioner. It means that this entity contains info about practitioner, network, location, organization and healthcareService. You can use PractitionerRole to search practitioners in the selected network:

1. Get practitionerRoles by network<br/>
   [https://portal.aidbox.myparamount.org/fhir/PractitionerRole?network=ff4f9bbc-8750-4fdd-bc80-a871d758f6e7](https://portal.aidbox.myparamount.org/fhir/PractitionerRole?network=ff4f9bbc-8750-4fdd-bc80-a871d758f6e7)	
2. Get Practitioner Fhir ID from the PractitionerRole entity
```json
"practitioner": {
  "id": "920c870c-2553-4ff0-b255-b2c58504dbce",
  "resource": {
    ...
  },
  "resourceType": "Practitioner"
}
```	
3. Get PractitionerRole by Fhir ID<br/>
[https://portal.aidbox.myparamount.org/fhir/PractitionerRole?id=c020618b-68ad-412c-b104-7c3db0e302d6](https://portal.aidbox.myparamount.org/fhir/PractitionerRole?id=c020618b-68ad-412c-b104-7c3db0e302d6)


#### Advanced PractitionerRole Queries

Also PractitionerRole entity is used to get all FHIR entities connected with a practitioner in one query. These queries can use multiple search parameters and you can include, exclude and combine them. Also you can control what entities will be returned by including and excluding entities from the _include parameter of these queries.

To add additional entities in the response, like Practitioner or Location you should use _include parameter, e.g.:

- Get PractitionerRole and Practitioner entities<br/>
[https://portal.aidbox.myparamount.org/fhir/PractitionerRole?_include=PractitionerRole:practitioner](https://portal.aidbox.myparamount.org/fhir/PractitionerRole?_include=PractitionerRole:practitioner)	
- Get PractitionerRole with Practitioner and Location entities<br/>
[https://portal.aidbox.myparamount.org/fhir/PractitionerRole?_include=PractitionerRole:practitioner,PractitionerRole:location](https://portal.aidbox.myparamount.org/fhir/PractitionerRole?_include=PractitionerRole:practitioner,PractitionerRole:location)			
- Get PractitionerRole with Practitioner and HealthcareService entities<br/>
[https://portal.aidbox.myparamount.org/fhir/PractitionerRole?_include=PractitionerRole:practitioner,PractitionerRole:service](https://portal.aidbox.myparamount.org/fhir/PractitionerRole?_include=PractitionerRole:practitioner,PractitionerRole:service)			
	
Also you can use these search parameters:	

- practitioner:name - practitioner name
- organization:name - organization name
- practitioner:network - practitioner network code
- practitioner:specialty - full practitioner specialty name
- practitioner:phone - practitioner phone
- practitioner:specialty - practitioner specialty code
- practitioner:location - practitioner location code

<!-
Advanced PractitionerRole queries examples:

- Get by practitioner name<br/>
[https://portal.aidbox.myparamount.org/fhir/PractitionerRole?_include=PractitionerRole:practitioner&practitioner:Practitioner.name=Yost%20Catherine](https://portal.aidbox.myparamount.org/fhir/PractitionerRole?_include=PractitionerRole:practitioner&practitioner:Practitioner.name=Yost%20Catherine)

- Get by all search parameters<br/>
[https://portal.aidbox.myparamount.org/fhir/PractitionerRole?_include=PractitionerRole:organization,PractitionerRole:practitioner,PractitionerRole:location,&practitionerName=SEQUEIRA%20RODRIGO&organizationName=THE%20MOUNT%20SINAI%20HOSPITAL&practitionerNetwork=DSNP&practitionerSpecialty=GENERAL%20SURGERY&practitionerType=SPECIALISTS&practitionerSpecialtyCode=21001&practitionerTypeCode=SP](https://portal.aidbox.myparamount.org/fhir/PractitionerRole?_include=PractitionerRole:organization,PractitionerRole:practitioner,PractitionerRole:network,PractitionerRole:location,PractitionerRole:healthcareService&practitionerName=SEQUEIRA%20RODRIGO&organizationName=THE%20MOUNT%20SINAI%20HOSPITAL&practitionerNetwork=DSNP&practitionerSpecialty=GENERAL%20SURGERY&practitionerType=SPECIALISTS&practitionerSpecialtyCode=21001&practitionerTypeCode=SP)
___

### Organization

We store information about organization in these FHIR Entities:

Organization - basic info about an organization. Contains name, address, type, specialty, identifiers like NPI and telecom info like phone and email.
OrganizationAffiliation - central entity to connect organization's entities.
Network - health plans an organization is connected with
Location - organization's location (address) and telecom (phone, email) info 
HealthcareService - services provided in an organization

Organization queries examples:

- Get 100 organizations (by default)<br/>
  [https://portal.aidbox.myparamount.org/fhir/Organization](https://portal.aidbox.myparamount.org/fhir/Organization)
- Get organization by name<br/>
  [https://portal.aidbox.myparamount.org/fhir/Organization?name=Partnership%20Health%20Center](https://portal.aidbox.myparamount.org/fhir/Organization?name=Partnership%20Health%20Center)
- Get organizations by address zip code<br/>
  [https://portal.aidbox.myparamount.org/fhir/Organization?address:postalCode=59801](https://portal.aidbox.myparamount.org/fhir/Organization?address:postalCode=59801)
- Get organizations by type<br/>
  [https://portal.aidbox.myparamount.org/fhir/Organization?type=prvgrp](https://portal.aidbox.myparamount.org/fhir/Organization?type=prvgrp)	
- Get organization by identifier<br/>
  [https://portal.aidbox.myparamount.org/fhir/Organization?identifier=71673](https://portal.aidbox.myparamount.org/fhir/Organization?identifier=71673)
- Get organizations by address AND type<br/>
  [https://portal.aidbox.myparamount.org/fhir/Organization?address=BRONX&type=prvgrp](https://portal.aidbox.myparamount.org/fhir/Organization?address=BRONX&type=prvgrp)


### OrganizationAffiliation

OrganizationAffiliation is a central entity for an organization. It means that this entity contains info about organization, network, location, and healthcareService. You can use OrganizationAffiliation to search organization in the selected network:

1. Get OrganizationAffiliation by network<br/>
  [https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?organizationNetwork=MLTC](https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?organizationNetwork=MLTC)	
2. Get Organization Fhir ID from the OrganizationAffiliation entity
```json	
"organization": {
     "id": "22d99f7c-4dc6-46da-b5f8-1371f6ae8a53",
     "resource": {
		...
     },
     "resourceType": "Organization"
}
```		
3. Get Organization by Fhir ID<br/>
  [https://portal.aidbox.myparamount.org/fhir/Organization?id=22d99f7c-4dc6-46da-b5f8-1371f6ae8a53](https://portal.aidbox.myparamount.org/fhir/Organization?id=22d99f7c-4dc6-46da-b5f8-1371f6ae8a53)

##### Advanced OrganizationAffiliation Queries

Also OrganizationAffiliation entity is used to get all FHIR entities connected with an organization in one query. These queries can use multiple search parameters and you can include, exclude and combine them. Also you can control what entities will be returned by including and excluding entities from the _include parameter of these queries.

To add additional entities in the response, like Organization or HealthcareService you should use _include parameter, e.g.:

- Get OrganizationAffiliation and Location entities<br/>
  [https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:location](https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:location)		
- Get OrganizationAffiliation with Location and HealthcareService entities<br/>
  [https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:location,OrganizationAffiliation:service](https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:location,OrganizationAffiliation:service)
- Get OrganizationAffiliation with all entities<br/>        
  [https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:location,OrganizationAffiliation:network,OrganizationAffiliation:location,OrganizationAffiliation:service](https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:location,OrganizationAffiliation:network,OrganizationAffiliation:location,OrganizationAffiliation:service)

Also you can use these search parameters:	
	
- organizationName - organization name
- organizationNetwork - organization network code
- organizationType - full organization type name
- organizationSpecialty - full organization specialty name
- organizationSpecialtyCode - organization specialty code
- organizationTypeCode - organization type code


Advanced OrganizationAffiliation queries examples:

- Get by organization name
<br/> 
[https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:organization,OrganizationAffiliation:network,OrganizationAffiliation:location,OrganizationAffiliation:service&organizationName=ALWAYS%20HOME%20CARE%20INC](https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:organization,OrganizationAffiliation:network,OrganizationAffiliation:location,OrganizationAffiliation:service&organizationName=ALWAYS%20HOME%20CARE%20INC)
- Get by network code and organization specialty
<br/> 
[https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:network,OrganizationAffiliation:location,OrganizationAffiliation:service&network=864e82d9-fba5-4923-ae8f-d18b24d573bd&specialty=193200000X](https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:organization,OrganizationAffiliation:network,OrganizationAffiliation:location,OrganizationAffiliation:service&organizationNetwork=MLTC&organizationSpecialty=HOME%20HEALTH%20AIDE)
- Get by all search parameters
<br/>  
[https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:organization,OrganizationAffiliation:network,OrganizationAffiliation:location,OrganizationAffiliation:service&organizationName=ALWAYS%20HOME%20CARE%20INC&organizationNetwork=MLTC&organizationType=ANCILLARY&organizationSpecialty=HOME%20HEALTH%20AIDE&organizationTypeCode=AN&organizationSpecialtyCode=66801](https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:organization,OrganizationAffiliation:network,OrganizationAffiliation:location,OrganizationAffiliation:service&organizationName=ALWAYS%20HOME%20CARE%20INC&organizationNetwork=MLTC&organizationType=ANCILLARY&organizationSpecialty=HOME%20HEALTH%20AIDE&organizationTypeCode=AN&organizationSpecialtyCode=66801)