---
title: 'Description'
---

# Paramount Interoperability APIs
Overview
Paramount interoperability APIs enable Paramount members to consent to have their health data shared with third-party applications. It also allows third-party application owners to connect to provider and pharmacy directories, further referred to as “public non-member specific data.”

## Paramount Interoperability APIs provide the following functionality:

Enable developers to register member-facing applications.
Enable members to provide consent for an application to access their data.
Use the HL7 Fast Healthcare Interoperability Resources (FHIR) standard for member data.
Use the HL7 FHIR standard for sharing public non-member specific data.
Third Party Applications
Developer-friendly, standards-based APIs that enable third party applications for vendors to connect their applications or programs to access Paramount data.

To use the Paramount interoperability API, a developer must register their application. An organization must register as a user and complete the registration application before submitting their application for consideration.


## API Permissions and Scopes
Access tokens have scopes, which define permissions and the resources that the token can access. Scopes are primarily utilized to determine the type of data an application is requesting. Scopes must be explicitly declared; wildcards are not supported.

In the current release the following scopes are available for the following types of requests:

- Public access - Provider Directory
- Permissioned based - Patient access

Note: Any Scope not currently listed is not supported.

This gives access to the correct FHIR Endpoints.

## API Documentation
This document serves the purpose of a quick start and provides useful links to the corresponding standards and specifications.

It does not provide detailed specification of the FHIR API or full details of its implementation in Aidbox.

## Basic Requests
Aidbox follows the FHIR standard. All API calls should be done using the following base url:

[http://hl7.org/fhir/](http://hl7.org/fhir/)

For provider access, that is public - [https://portal.aidbox.myparamount.org/fhir](https://portal.aidbox.myparamount.org/fhir)

For patient access, that is restricted and requires permissions - [https://portal.aidbox.myparamount.org/smart](https://portal.aidbox.myparamount.org/smart)

Below are examples of basic requests, a full description of which can be found in the RESTful API section of the specification.

Find additional information about Aidbox and its implementation of the standard:

[http://hl7.org/fhir/http.html](http://hl7.org/fhir/http.html)

[https://docs.aidbox.app/](https://docs.aidbox.app/)

### Read

To read data you should use GET HTTP request with the following basic structure:

GET [base url]/[resource name]

Where

[base url] - the base url (see above)

[resource name] - is the name of a resource you want to read.



## Standard Search Parameters
Search parameters can be one of the search parameters defined for a particular resource in the standard. For example, for the practitioner resource the list of search parameters can be found here:

[http://hl7.org/fhir/practitioner.html#search](http://hl7.org/fhir/practitioner.html#search)

Or, for the organization resource here:

[https://hl7.org/fhir/organization.html#search](https://hl7.org/fhir/organization.html#search)

For example, to find the practitioner by name you can use the following request:

GET [base url]/Practitioner?name=John

Or to find the practitioner by it’s identifier (for example NPI) use the following request:

GET [base url]/Practitioner?identifier=1111111111

## Special Search Parameters
Search parameters can be one of the following special search parameters:

| Parameter    | Type | Description |
| ------------- | ------------- | ------------- |
| _id          | FHIR  | Search and sort by resource id |
| _lastUpdated | FHIR  | Search and sort by resource last modification date  |
| _text        | FHIR  | Full text search by resource narrative |
| _content     | FHIR  | Full text search by resource content |
| _ilike       | ILIKE | search by resource content |
| _elements    | FHIR+ | Include or exclude specific resource elements |
| _summary     | FHIR  | Include only summary elements |
| _list        | FHIR  | Search resources included into specific List |
| _sort        | FHIR  | Sort search results |
| _total       | FHIR  | Turn on/off total count |
| _include     | FHIR  | Include referenced resources into result |
| _revinclude  | FHIR  | Include into result resources, which reference searched resources |
| _explain     |       | See query execution plan |
| _result      |       | Change result format |


For example, to use full text search to find a practitioner, use the following query:

GET [base url]/Practitioner?_content=John

Learn more about special search parameters:

[https://docs.aidbox.app/api-1/fhir-api/search-1#special-parameters](https://docs.aidbox.app/api-1/fhir-api/search-1#special-parameters)

Authentication and Authorization
Provider and pharmacy directories are publicly available information and do not require any additional security measures. Members’ claims and clinical data are considered Protected Health Information (PHI) and need to be secured.

Tutorial for additional help:

[https://docs.aidbox.app/app-development-guides/tutorials/authentication-and-authorization#checking-authorization](https://docs.aidbox.app/app-development-guides/tutorials/authentication-and-authorization#checking-authorization)

Implementation Guides for CMS Interoperability Rule
The FHIR standard provides a set of resources and its attributes, but in most

cases it does not impose strict restrictions on the required attributes and their values. In turn, implementation guides impose additional, more stringent restrictions. The following 4 IGs are used to comply with CMS Rule (https://www.cms.gov/Regulations-and-Guidance/Guidance/Interoperability/index):

Provider Directory API

[http://hl7.org/fhir/us/davinci-pdex-plan-net/index.html](http://hl7.org/fhir/us/davinci-pdex-plan-net/index.html)

Drug Formulary

[http://hl7.org/fhir/us/davinci-drug-formulary/](http://hl7.org/fhir/us/davinci-drug-formulary/)

Clinical Data

[http://hl7.org/fhir/us/core/history.html](http://hl7.org/fhir/us/core/history.html)

Claims and Encounter Data

[http://hl7.org/fhir/us/carin-bb/index.html](http://hl7.org/fhir/us/carin-bb/index.html)

Provider and pharmacy directories are publicly available information and do not require any additional security measures. Members’ claims and clinical data are considered Protected Health Information (PHI) and need to be secured. Members authorize applications they want to use to access their PHI. The process of app registration and authorization by members is standardized in the SMART on FHIR specification.

SMART App Launch Framework (hl7.org)