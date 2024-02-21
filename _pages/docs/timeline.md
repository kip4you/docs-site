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

#### Timeline Elements

![Timeline visualization](assets/images/timeline/timeline-visualization.png)

To start the explanation of the timeline, we need to highlight some important elements on the timeline. 

An important concept here to highlight is that the timeline <b>is not composed of tasks</b> but rather <b>steps</b>. Each of the steps, as shown in the image above, is an abstraction representing a <b>set of tasks</b> defined during the timeline creation. This set can contain a <b>single task or multiple tasks</b> for a step of the timeline.

Another thing to mention is the indication of colors during the timeline visualization and their meaning. The <b>gray</b> point indicates that the task has <b>not started</b>. The <b>blue</b> point one indicates that the task has been assigned to someone and <b>started</b>, and finally, the <b>green</b> point indicates that the task has been <b>completed</b>.

#### Multiple Timelines

During timeline creation, we may encounter situations in the process where we'll have multiple timelines. Using a simple Travel Plan process as an example, we can observe an exclusive gateway where if the person indicates that they need to rent a hotel for the trip, we will have one more task to follow, thus having <b>two possible timelines</b>.

![Travel Plan](assets/images/timeline/bpmn-travel-plan.png)

In the image below, we have an example of creating the first timeline for the same process. Since it's the first timeline, <b>we don't need to define any timeline condition</b>. Only steps are created for choosing the flight and renting a car, choosing the path where it's not necessary to rent a hotel room.

##### Default timeline path

![Timeline Default Path](assets/images/timeline/timeline-default-path.png)

![Timeline Default Path view](assets/images/timeline/timeline-view-default-path.png)

As we can see, by choosing the option not to book a hotel room, the timeline will follow the default flow.

##### Alternative timeline path

![Timeline Condition Alternative Path](assets/images/timeline/timeline-condition-alternative-path.png)

![Timeline Alternative Path](assets/images/timeline/timeline-alternative-path.png)

![Timeline Alternative Path view](assets/images/timeline/timeline-alternative-path-view.png)

Whereas if we book a hotel room, the timeline will switch to the flow containing the condition that checks if booking a hotel room is marked as YES, altering the appearance of the timeline and including the step of Booking a Hotel.

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

Firstly, on the right-hand side of the page, you can view the Task Definition Keys, which are the IDs of all tasks included in your BPMN. Additionally, you can use the button to copy the task definition key for use in the step expression field as we will talk next.

#### Task Definition Key
![Timelines delete](assets/images/timeline/timeline-task-definition-key.png)

Below the Task Definition Keys listing, we find examples of expressions that can be used to construct a step of a timeline. Thus, we have different ways to represent a step in the timeline, which can be a single task as a focus for that step, or tasks with <b>'AND'</b> and <b>'OR'</b> conditions, <b>with the option to use parentheses to include more than one task</b>. This variety of options allows us to summarize and simplify the understanding of a process that would otherwise be complex, making it more easily understandable and visually appealing.

#### Timeline Expression Examples
![Timelines examples](assets/images/timeline/timeline-examples.png)

To create the timeline, we have two initial fields. The first one is the <b>"Timeline Name"</b>, where you provide a suggestive name to identify the timeline. The second field is <b>"Timeline Condition"</b>, where you insert an expression that determines which timeline should be used when you have multiple timelines for the process. See section 'Multiple Timelines' for more details.

<b> It's important to remember that the first timeline doesn't need to include a timeline condition, as it will define a default flow for the process. </b>

#### Timeline Default Creation
![Timelines default](assets/images/timeline/timeline-default-creation.png)

#### Timeline with timeline Condition
![Timelines with condition](assets/images/timeline/timeline-with-condition.png)

#### Timeline Customization Options

During the timeline creation, we have some customization options where we can define the <b>step's name</b>, along with the <b>expression</b> which, as mentioned earlier, can include a single task or multiple tasks through the expressions. Additionally, we have three buttons: one with an <b>upward arrow</b>, indicating that you can move a step up, or down if you press the <b>downward arrow</b>. Furthermore, we can <b>delete</b> a step if necessary by pressing the button with a trash can icon.

![Timelines customization](assets/images/timeline/timeline-customization.png)

### 4. Timeline visualization in a process

To visualize the timeline, simply access the process instance for which a timeline has been created, and it will load the timeline horizontally, showing the progress of the process linearly.

![Timelines examples](assets/images/timeline/timeline-process-instance.png)