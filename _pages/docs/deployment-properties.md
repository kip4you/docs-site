---
layout: single
permalink: /deployment-properties
last_modified_at: 2022-08-07
toc: true
sidebar:
  nav: "docs"
---

# Deployment properties

Deployment properties are a mechanism used in our platform to control variability in processes. 


## Basic Usage

Create a process using Camunda Modeler and in the tab XPTO insert a property called YYYYY with a default value XXXX.
When you deploy this process into the AKIP App, the platform scanned the model looking for properties and register them as deployment properties. 
After that, you can change the default value using the form presented in the deployment page.


## Example Basic Usage




## Deployment Properties and Tenant

Another common use of deployment properties is associated with Tenant. For example, in a scenario where two tenants follow similar processes, we can have one process model whose variability is controlled by deployment properties. 

## Example Deployment Properties and Tenants