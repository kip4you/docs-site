---
layout: single
permalink: /timeline
last_modified_at: 2024-02-19
toc: true
sidebar:
  nav: "docs"
---

# Timeline

## What is the timeline?

The timeline is a tool designed to simplify the visualization of a process as a whole, enabling users with less familiarity in BPMN to understand the progress of the process in a linear manner. This allows tracking of ongoing tasks, completed tasks, and those that are still pending.

## How to use the timeline?

### 1. Accessing the timeline of a process

To set up the timeline, you first need to decide which process it will be used for and then access the listing and configuration through the Process Definition screen, located under the 'Timelines' button.

#### Button Timelines
![Button timelines](assets/images/timeline/button-timelines.png)

### 2. Timelines

When you click the button, you'll be directed to a page listing the information of the timelines created for that process. On this page, you can <b>view</b>, <b>edit</b>, and <b>delete</b> a specific timeline. If you wish to configure a new timeline, simply click on the 'Create a new timeline' button.


#### Timelines page
![Timelines page](assets/images/timeline/timelines-page.png)

#### Timeline view
![Timelines view](assets/images/timeline/timeline-view.png)

#### Timeline edit
![Timelines edit](assets/images/timeline/timeline-edit.png)

#### Timeline delete
![Timelines delete](assets/images/timeline/timeline-remove.png)

### 3. Creating a new timeline

On the timeline creation page, we should focus on certain information displayed on the screen.

Firstly, on the right-hand side of the page, you can view the Task Definition Keys, which are the IDs of all tasks included in your BPMN. Additionally, you can use the button to copy the task name for use as I'll mention next.

#### Task Definition Key
![Timelines delete](assets/images/timeline/timeline-task-definition-key.png)

Below the Task Definition Keys listing, we find various examples of expressions that can be used to construct our timeline. Thus, we have different ways to represent a step in the timeline, which can be a single task as a focus for that step, or tasks with <b>'AND'</b> and <b>'OR'</b> conditions, <b>with the option to use parentheses to include more than one task</b>. This variety of options allows us to summarize and simplify the understanding of a process that would otherwise be complex, making it more easily understandable and visually appealing.

#### Timeline Expression Examples
![Timelines examples](assets/images/timeline/timeline-examples.png)

To create the timeline, we have two initial fields. The first one is the <b>"Timeline Name"</b>, where you provide a suggestive name to identify the timeline. The second field is <b>"Timeline Condition"</b>, where you insert an expression that determines other task flows you want to follow in the timeline. Since the visualization of the timeline is linear, it is necessary to define these other flows so that <b>when a specific condition of the timeline is met, the visualization changes to follow a specific flow.</b>

<b> It's important to remember that the first timeline doesn't need to include a timeline condition, as it will define a default flow for the process. </b>

#### Timeline Default Creation
![Timelines default](assets/images/timeline/timeline-default-creation.png)

#### Timeline with timeline Condition
![Timelines with condition](assets/images/timeline/timeline-with-condition.png)

### 4. Timeline visualization in a process

To visualize the timeline, simply access the process instance for which a timeline has been created, and it will load the timeline horizontally, showing the progress of the process linearly.

#### Example of a timeline working
![Timelines examples](assets/images/timeline/timeline-process-instance.png)

The blue point one indicates that the task has been assigned to someone and is in <b>progress</b>. The green point indicates that the task has been <b>completed</b>, and finally, the gray point indicates that the task has <b>not yet started</b>.