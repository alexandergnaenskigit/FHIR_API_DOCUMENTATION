---
title: '2. Provider Directory API'
---

# Provider Directory API

Provider Directory API follows [DaVinci PDEX Plan Net Implementation Guide](http://hl7.org/fhir/us/davinci-pdex-plan-net/index.html)  

This implementation guide defines a FHIR interface to a health insurer’s insurance plans, their associated networks, and the organizations and providers that participate in these networks. Publication of this data through a standard FHIR-based API will enable third parties to develop applications through which consumers and providers can query the participants in a payer’s network that may provide services that address their health care needs. Although there are multiple types and sources of providers’ directories, including provider organizations (i.e., a hospital listing all its physicians), government (i.e., listing of providers in Medicare), payers (i.e., a health plan’s provider network), and third-party entities (such as vendors that maintain provider directories), the focus of this implementation guide is on Payer Provider Directories.


## Practitioner

The information about practitioners is stored in these FHIR Entities:

- [Practitioner](../../profiles/Practitioner/DaVinci-PDEX-Plan-Net.html) - basic info about а practitioner. Contains demographics, specialty, language and identifiers like NPI and IRS
- [PractitionerRole](../../profiles/PractitionerRole/DaVinci-PDEX-Plan-Net.html) - central entity to connect practitioner's entities. Also contains info about available time
- [Organization](../../profiles/Organization/DaVinci-PDEX-Plan-Net.html) - practitioner's place of work
- [Location](../../profiles/Location/DaVinci-PDEX-Plan-Net.html) - practitioner's location info (address) and telecom info (phone, email) 
- [HealthcareService](../../profiles/HealthcareService/DaVinci-PDEX-Plan-Net.html) - services provided by a practitioner

### Sample Queries

Practitioner queries examples:

- Get 100 practitioners (by default)<br/>
  [https://portal.aidbox.myparamount.org/fhir/Practitioner](https://portal.aidbox.myparamount.org/fhir/Practitioner)
- Get practitioner by name<br/>
  [https://portal.aidbox.myparamount.org/fhir/Practitioner?name=Garner%20Melanie](https://portal.aidbox.myparamount.org/fhir/Practitioner?name=Garner%20Melanie)
- Get practitioner by NPI<br/>
  [https://portal.aidbox.myparamount.org/fhir/Practitioner?identifier=1033572763](https://portal.aidbox.myparamount.org/fhir/Practitioner?identifier=1033572763)


### PractitionerRole

PractitionerRole is a central entity which connects info about practitioner, network, location, organization and healthcareService. You can use PractitionerRole to search practitioners in the selected network:

1. Get practitionerRoles by organization<br/>
   [https://portal.aidbox.myparamount.org/fhir/PractitionerRole?organization=98fd97ef-0863-4b89-a951-3f52cc639543](https://portal.aidbox.myparamount.org/fhir/PractitionerRole?organization=98fd97ef-0863-4b89-a951-3f52cc639543)	
2. Get Practitioner Fhir ID from the PractitionerRole entity
```json
"practitioner": {
  "id": "694b0dc1-b8fd-41b6-99a9-62681b28fa49",
  "resource": {
    ...
  },
  "resourceType": "Practitioner"
}
```	
3. Get PractitionerRole by Fhir ID<br/>
[https://portal.aidbox.myparamount.org/fhir/PractitionerRole?practitioner=694b0dc1-b8fd-41b6-99a9-62681b28fa49](https://portal.aidbox.myparamount.org/fhir/PractitionerRole?practitioner=694b0dc1-b8fd-41b6-99a9-62681b28fa49)


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

## Organization

We store information about organization in these FHIR Entities:

- [Organization](../../profiles/Organization/DaVinci-PDEX-Plan-Net.html) - basic info about an organization. Contains name, address, type, specialty, identifiers like NPI and telecom info like phone and email.
- [OrganizationAffiliation](../../profiles/OrganizationAffiliation/DaVinci-PDEX-Plan-Net.html) - central entity to connect organization's entities.
- [Location](../../profiles/Location/DaVinci-PDEX-Plan-Net.html) - organization's location (address) and telecom (phone, email) info 
- [HealthcareService](../../profiles/HealthcareService/DaVinci-PDEX-Plan-Net.html) - services provided in an organization

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

OrganizationAffiliation is a central entity which connects info about organization, network, location, and healthcareService. You can use OrganizationAffiliation to search organization in the selected network:

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
[https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:network,OrganizationAffiliation:location,OrganizationAffiliation:service&network=75ca8a25-2914-42c3-9022-af3236e6b2cb&specialty=193200000X](https://portal.aidbox.myparamount.org/fhir/OrganizationAffiliation?_include=OrganizationAffiliation:network,OrganizationAffiliation:location,OrganizationAffiliation:service&network=75ca8a25-2914-42c3-9022-af3236e6b2cb&specialty=193200000X)
