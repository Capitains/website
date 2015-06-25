---
layout: page
title: "Ahab"
group: navigation
description: "Description of the Ahab Service Norm"
---
{% include JB/setup %}

## Introduction

Ahab has implementations for [eXistDB restxq](http://github.com/Capitains/Ahab-eXistDB) and a [cache layer written for Flask](http://github.com/Capitains/Ahab) (Python web app). Ahab provides new functionnalities to CTS repositories, using CTS as its basic informations.

Addition to Ahab are welcome, either as implementations or as requests ! Ahab is a norm, not a software !

## Implemantations

- [Ahab-ExistDB](http://github.com/Capitains/Ahab-eXistDB) : Implementation of the Ahab API for eXistDB restxq services

Others :

- [Ahab for Flask](http://github.com/Capitains/Ahab) : Ahab for Flask is mostly a cache layer that you can add on top of your implementations. Ahab for eXistDB being quite slow for big requests, the addition of a strong cache layer between the API and the user allowed for better performances.

## Requests

Ahab supports two different URL naming convention, and both should be supported by implementations : a RESTful one and a "GET" one.

- "GET" request should accept a `request` url parameter to specify the request to do. All other request parameters would be added normally. *e.g.* `http://localhost/ahab?request=Search&query=lasciv*&urn=urn:cts:latinLit:phi1294`
- REST request should be written as : `/ahab/rest/v1.0/*requestname*/`. Further details are given for each request when applicable.

### Search
**Purpose**: Search proposes to do fulltext search on a specific area of a CTS API.

| Parameter | Type | Required/optional | Description |  
|  ------   | ---- | ----------------- | ----------- | 
| urn       | str  | Required          |  |
| query     | str  | Required          |  |
| start     | int  | Optional          |  |
| limit     | int  | Optional          |  |

**XML Reply schema**: 

**JSON Reply schema**: 

### Permalink
**Purpose**: Permalink is a tool to help retrieve a urn on a CTS api. CTS API are based on the prerequisite to know the right inventory. If the API has more than one inventory, having this tool can help external users to find a text without knowing their inventory.

| Parameter | Type | Required/optional | Description |  
|  ------   | ---- | ----------------- | ----------- | 
| urn       | str  | Required          |  |
| query     | str  | Required          |  |

**Reply schema**: 
