---
layout: single
permalink: /notify
last_modified_at: 2023-08-24
toc: true
sidebar:
  nav: "docs"
---

# Notify 

Notification is a key element in many processes.
To facilitate the management of notifications, the platform
provides a sophisticated mechanism to handle this functionality.

## Overview

Notifications is a feature defined in the creation of the BPMN process 
using the Camunda tool and can be used in 3 situations for the user Assignee, 
CandidateGroups and CandidateUsers.

## Configuration

To use the notify functionality when creating the BPMN process with camunda and the selected task, 
access the right side tab with the name properties panel just after the top tab General and Details as shown in the example below.

![Config Notify](assets/images/configNotify.png)

In the Assignee, CandidateGroups and CandidateUsers fields you can assign a notify by directly placing the username 
in the field or through a delegate expression which will be found in the side tab Properties Panel top tab Listeners 
as shown in the example below.

![Exemple Delegate_Expression](assets/images/exempleDelegateExpression.png)

In the Task Listener field you can create a delegate expression by clicking on the "+" symbol.

In the Event Type field you can select the desired wind in which notify will be executed.

In the field Listener Type you must select Delegate Expression.

In the field Delegate Expression you must put an expression present in the [Delegates](#delegates).

Or you can select an already created delegate expression and delete it by clicking on the "x" symbol.

## Delegates

#### `${akipNotifyAssigneeDelegate}`

#### `${akipNotifyCandidateGroupsDelegate}`

#### `${akipNotifyCandidateUsersDelegate}`

## Customizing notify
Notifications can be customized by accessing the src/resources/i18n/messages.propeties folder
as shown in the example below

![Exemple Customization](assets/images/exampleCustomization.png)