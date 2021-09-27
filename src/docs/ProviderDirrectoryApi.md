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

- Get by practitioner name and organization id<br/>
[https://portal.aidbox.myparamount.org/fhir/PractitionerRole?_include=PractitionerRole:organization,PractitionerRole:practitioner&practitioner:Practitioner.name=Yost%20Catherine&organization:Organization.id=1a39a0ac-d3af-41c5-bc1e-3f69e1301814](https://portal.aidbox.myparamount.org/fhir/PractitionerRole?_include=PractitionerRole:organization,PractitionerRole:practitioner&practitioner:Practitioner.name=Yost%20Catherine&organization:Organization.id=1a39a0ac-d3af-41c5-bc1e-3f69e1301814)
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
  [https://portal.aidbox.myparamount.org/OrganizationAffiliation?network=75ca8a25-2914-42c3-9022-af3236e6b2cb](https://portal.aidbox.myparamount.org/OrganizationAffiliation?network=75ca8a25-2914-42c3-9022-af3236e6b2cb)	
2. Get Organization Fhir ID from the OrganizationAffiliation entity
```json	
"organization": {
     "id": "e05865d3-cbde-4bab-92f6-a41d263efb79",
     "resource": {
		...
     },
     "resourceType": "Organization"
}
```		
3. Get Organization by Fhir ID<br/>
  [https://portal.aidbox.myparamount.org/fhir/Organization/e05865d3-cbde-4bab-92f6-a41d263efb79](https://portal.aidbox.myparamount.org/fhir/Organization/e05865d3-cbde-4bab-92f6-a41d263efb79)

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
	
- organization: name - organization name
- organization: network - organization network code
- organization: telecom - organization phone
- organization: specialty - full organization specialty name
- organization: email - organization email


Advanced OrganizationAffiliation queries examples:

- Get by network code and organization specialty
<br/> 
[https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:network,OrganizationAffiliation:location,OrganizationAffiliation:service&network=864e82d9-fba5-4923-ae8f-d18b24d573bd&specialty=193200000X](https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:organization,OrganizationAffiliation:network,OrganizationAffiliation:location,OrganizationAffiliation:service&organizationNetwork=MLTC&organizationSpecialty=HOME%20HEALTH%20AIDE)
