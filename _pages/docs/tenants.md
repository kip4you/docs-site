---
layout: single
permalink: /tenants
last_modified_at: 2022-08-07
toc: true
sidebar:
  nav: "docs"
---

# Working with Tenants

Working with Tenants is one of the most important features of the KIP4You PAP. 
A Tenant represents a subgroup inside the process engine that is used to control basically two aspects:

* Scope
* Variability

## Scope

Let's consider that we have two or more departments inside a given organization and that each department should not see process elements from other departments (process instances and tasks).
In this scenarion, a tenant is a concept used to control the scope of each department.
So, in our platform we create a tenant to each department and so the visibility of the process objects (process instances and tasks) is controlled by tenant.


## Variability

Another motivation for this feature is related to variability. Imagine a scenario where two departments follow almost the same process but there is a variation between them. 
In that case, we can deploy two different processes that share forms and delegates but are in fact different. 


## Managing Tenants

The platform has native CRUD features to manage tenants that can be accessed through the menu *Administration -> Tenants*.


## Managing Tenant Members

This feature allows to manage the members of a given tenant. 

## Example

- Create two process models that share the same identifier and components but that have a small variability.
- Create the forms and delegates for the processes
- Deploy the processes to different tenants
- Start process using different users to check the behaviour.
