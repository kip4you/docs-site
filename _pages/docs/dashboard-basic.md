---
layout: single
permalink: /dashboards-basic
last_modified_at: 2022-08-07
toc: true
sidebar:
  nav: "docs"
---

# Basic Dashboards

The platform currently has 4 dashboard groups with information related to process instances metrics, process tenants, average unassigned task time, and average task completion time.

### Group 1: Boxes

The first one is the boxes, by default, the project comes with a component on the dashboard containing 6 boxes with information on Process Instances Metrics. Among this information, we have how many processes were created, how many processes are active, how many processes were canceled, how many processes were completed, the mean time to completion, and the total of this.

![Boxes](assets/images/dashboard-basic/boxes.png)

### Group 2: Charts

The second component is the charts, by default, the project comes with 3 different card with a table, bar chart and a pie chart.

#### Processes by Tenant

This card contains the information about the Tenant of the process and the number of the instances running in this process.

![Processes by Tenant](assets/images/dashboard-basic/dashboard-basics-processes-by-tenant.png)

#### Tasks Mean Unassigned Time

This card contains information about the tasks of the process displaying the time when the task is not assigned to anyone using Business Hours (8 hours) and Total Hours (24 hours) as well.

![Unassigned table](assets/images/dashboard-basic/dashboard-basics-unassigned-table.png)

![Unassigned charts](assets/images/dashboard-basic/dashboard-basics-unassigned-chart.png)

#### Tasks Mean Time to Completion

Continuing with the default chart cards, we have the Mean Time to Completion. As the name suggests, this card displays the mean time to complete a task in Business Hours (8 hours), in Total (24 hours), and also shows the number of task executions in the process.

![Completion table](assets/images/dashboard-basic/dashboard-basics-completion-table.png)

![Completion chart 01](assets/images/dashboard-basic/dashboard-basics-completion-chart-1.png)

![Completion chart 02](assets/images/dashboard-basic/dashboard-basics-completion-chart-2.png)

#### Other Tasks of the process

During the execution of tasks, each of them will start to be displayed on the dashboard containing the same information as the previous cards: number of executions, mean time to complete in business hours (8 hours), and mean time to complete in total (24 hours).

In this example we can see 2 tasks Choose a Flight of the Travel Plan Process:

![Task table](assets/images/dashboard-basic/dashboard-basics-task-table.png)

![Task chart 01](assets/images/dashboard-basic/dashboard-basics-task-chart-1.png)

![Task chart 02](assets/images/dashboard-basic/dashboard-basics-task-chart-2.png)
