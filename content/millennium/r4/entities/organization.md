---
title: Organization | R4 API
---

# Organization

* TOC
{:toc}

## Overview

The Organization resource describes a grouping of people or business entities relevant to the healthcare process.  Organizations include hospitals, employers, insurance companies, physicians’ offices, rehabilitation facilities, laboratories, etc.

The following fields are returned if valued:

* [Organization Identifier](https://hl7.org/fhir/r4/organization-definitions.html#Organization.identifier){:target="_blank"}
* [Active](https://hl7.org/fhir/r4/organization-definitions.html#Organization.active){:target="_blank"}
* [Type](https://hl7.org/fhir/r4/organization-definitions.html#Organization.type){:target="_blank"}
* [Name](https://hl7.org/fhir/r4/organization-definitions.html#Organization.name){:target="_blank"}
* [Contact Information](https://hl7.org/fhir/r4/organization-definitions.html#Organization.telecom){:target="_blank"}
* [Address](https://hl7.org/fhir/r4/organization-definitions.html#Organization.address){:target="_blank"}

## Terminology Bindings

<%= terminology_table(:organization, :r4) %>

## Search

Search for Organizations that meet supplied query parameters:

    GET /Organization?:parameters

### Authorization Types

<%= authorization_types(provider: true, patient: true, system: true) %>

### Parameters

 Name        | Required?                               | Type       | Description
-------------|-----------------------------------------|------------|----------------------------------------------------------
 `_id`       | This or `identifier` or `type`          | [`token`]  | The logical resource id associated with the resource.
 `identifier`| This or `type` or `_id`                 | [`token`]  | NPI, OID or FederalTAXID identifier for the organization.
 `type`      | This or `identifier` or `_id`           | [`token`]  | The organization's type. Example: `http://terminology.hl7.org/CodeSystem/organization-type|govt`
 [`_count`]  | No                                      | [`number`] | The maximum number of results to return. Defaults to `100`.
 `name`      | This or `_id` or `identifier` or `type` | [`string`] | Name used for the organization.

 Notes:

- The `identifier` parameter
  - Code details are required. System is optional. If system is not provided, search is performed across all systems supported by the 
    Organization resource.
  - When valid system is provided, search is performed against the specific system.
  - When invalid system is provided, 400 bad request is returned.

### Headers

<%= headers fhir_json: true %>

### Example

#### Request

    GET https://fhir-open.cerner.com/r4/ec2458f2-1e24-41c8-b71b-0e701af7583d/Organization?_id=675844

#### Response

<%= headers status: 200 %>
<%= json(:r4_organization_bundle) %>

<%= disclaimer %>

### Errors

The common [errors] and [OperationOutcomes] may be returned.

[`string`]: https://hl7.org/fhir/R4/search.html#string

## $get-cg-for-mrcu

Search for Caregiver Organizations that meet supplied query parameters:
 
    GET /Organization/$get-cg-for-mrcu?:parameters

### Authorization Types

<%= authorization_types(provider: true, patient: true, system: true) %>

### Parameters

 Name        | Required?                      | Type       | Description
-------------|--------------------------------|------------|----------------------------------------------------------
 `_id`       | Yes                            | [`token`]  | The id of the care unit organization.

Notes:

* Only a single `_id` parameter can be provided.

### Headers

<%= headers fhir_json: true %>

### Example

#### Request

    GET https://fhir-open.cerner.com/r4/ec2458f2-1e24-41c8-b71b-0e701af7583d/Organization/$get-cg-for-mrcu?_id=3304067

#### Response

<%= headers status: 200 %>
<%= json(:r4_organization_caregiver_search_bundle) %>

<%= disclaimer %>

### Errors

The common [errors] and [OperationOutcomes] may be returned.

## Retrieve by id

List an individual Organization by its id:

    GET /Organization/:id

### Authorization Types

<%= authorization_types(provider: true, patient: true, system: true) %>

### Headers

<%= headers fhir_json: true %>

### Example

#### Request

    GET https://fhir-open.cerner.com/r4/ec2458f2-1e24-41c8-b71b-0e701af7583d/Organization/675844

#### Response

<%= headers status: 200 %>
<%= json(:r4_organization_entry) %>

<%= disclaimer %>

### Errors

The common [errors] and [OperationOutcomes] may be returned.

## Create

Create new Organization.

    POST /Organization

_Implementation Notes_

* Only the body fields mentioned below are supported. Unsupported fields will be ignored.

### Authorization Types

<%= authorization_types(provider: true, system: true) %>

### Headers

<%= headers head: {Authorization: '&lt;OAuth2 Bearer Token>', 'Content-Type': 'application/fhir+json'} %>

### Body Fields

<%= definition_table(:organization, :create, :r4) %>

### Example

#### Request

    POST https://fhir-ehr-code.cerner.com/r4/ec2458f2-1e24-41c8-b71b-0e701af7583d/Organization

#### Body

<%= json(:r4_organization_create) %>

#### Response

<%= headers status: 201 %>
<pre class="terminal">
Cache-Control: no-cache
Content-Length: 0
Content-Type: text/html
Date: Wed, 14 Aug 2019 17:23:14 GMT
Etag: W/"6767735"
Location: https://fhir-ehr-code.cerner.com/r4/ec2458f2-1e24-41c8-b71b-0e701af7583d/Organization/6767735
Last-Modified: Wed, 14 Aug 2019 17:23:14 GMT
Vary: Origin
X-Request-Id: 11111111111111111111111111111111
</pre>

The `ETag` response header indicates the current `If-Match` version to use on a subsequent update.

<%= disclaimer %>

### Errors

The common [errors] and [OperationOutcomes] may be returned.

[`_count`]: https://hl7.org/fhir/r4/search.html#count
[`token`]: http://hl7.org/fhir/r4/search.html#token
[`number`]: https://hl7.org/fhir/r4/search.html#number
[errors]: ../../#client-errors
[OperationOutcomes]: ../../#operation-outcomes
