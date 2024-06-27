---
layout: single
permalink: /dashboards-on-the-fly
last_modified_at: 2022-08-07
toc: true
sidebar:
  nav: "docs"
---

# On-the-fly Dashboards

On-the-fly dashboards are a sofisticated category of dashboards that can be configured during runtime.

### How to use

Accessing the settings of the chosen process dashboard, we can view several of the component groups for the dashboard that are already created by default or have been created from boxes and charts. At the bottom of the page, we can see an <b>"Add Group"</b> button that, when clicked, will open a new group.

![Group Builder](assets/images/dashboard-on-the-fly/dashboard-on-the-fly-group.png)

Initially, we fill in with a title that will be displayed on the generated dashboard card, and in the Group Builder field, we should fill in as follows: <b>akipDashboardCustomBoxGroupBuilder</b>.  By doing this, a new <b>Groovy-type field</b> will appear called **Group Builder Expression**, and it is in this field that we will define how our box will be generated on the fly.

![Custom Group Builder](assets/images/dashboard-on-the-fly/dashboard-on-the-fly-custom-group-builder.png)

## Basic Usage

### Custom Box Group Builder

For this, we have an example for setting up 3 simple boxes with fixed values **using groovy**. It's worth noting that the attributes for creating a box are title and value.

```groovy
def buildBoxList() {
    List<Map<String, Object>> boxes = new ArrayList<>()
    
    Map<String, Object> box1 = new HashMap<>()
    box1.put("title", "Box 1")
    box1.put("value", 10)
    boxes.add(box1)
    
    Map<String, Object> box2 = new HashMap<>()
    box2.put("title", "Box 2")
    box2.put("value", 20)
    boxes.add(box2)
    
    Map<String, Object> box3 = new HashMap<>()
    box3.put("title", "Box 3")
    box3.put("value", 30)
    boxes.add(box3)
    
    return boxes
}

def boxesList = buildBoxList()
```

Once we have defined our Groovy script, we simply need to click the Save button to visualize our created dashboard component.

![Basic Boxes](assets/images/dashboard-on-the-fly/dashboard-on-the-fly-basic-box.png)

## Advanced Usage

In the advanced usage of the On The Fly Dashboard, we have several ways to assemble our dashboard using the <b>groovy</b> together with the <b>bindingBuilder</b> for that purpose.

With it, we can use different variables to customize information on our dashboard, among them we have:

#### env

With Environment, we can utilize the information from <b>getActiveProfiles()</b>, which returns, as the name suggests, an array of strings representing the active profiles, and also <b>getDefaultProfiles()</b> to return default profiles of the project. All of this can be utilized by Groovy in generating an on-the-fly dashboard using the runtime.

#### hqlApi

With hqlApi, we can use queries to return both a <b>specific object</b> using **findObject("QUERY")** or a <b>list</b> using **findList("QUERY")** from database queries of the project. This option is likely to be the most used for creating dashboards on the fly.

#### jsonApi

This variable is for use in the **JSON conversion/representation** of an object, formatting it as a string.

#### messageApi

The variable from the messageApi can be used to utilize the getMessage method, which **returns a message corresponding to the provided key** (String type parameter key required). It uses the messageSource to retrieve the message with the specified key and returns the message using the default language of the operating system. If the message is not found, it returns null.

#### Examples

Here we have an example of a Groovy dashboard on the fly using the variable from hqlApi to query the database and bring information to our dashboard. For this, as seen previously in the Group Builder field of dashboard creation, we put the name **akipDashboardCustomBoxGroupBuilder** and fill the **Group Builder Expression** with the following Groovy code for example:

```groovy
import java.time.LocalDate
import java.time.LocalDateTime
import java.time.format.DateTimeFormatter

LocalDateTime startDateTime = dashboardRequest.getStartDateTime()

LocalDate startDate = startDateTime.toLocalDate()

String formattedStartDate = startDate.format(DateTimeFormatter.ofPattern("yyyy-MM-dd"))

def query = "SELECT tp.startDate, tp.name FROM TravelPlan tp WHERE tp.startDate >= '" + formattedStartDate + "'"

def resultList = hqlApi.findList(query)

List<Map<String, Object>> boxes = new ArrayList<>()
resultList.each { result ->
  Map<String, Object> box = new HashMap<>()
  box.put("title", result[1])
  box.put("value", "Start ${result[0]}")
  boxes.add(box)
}

return boxes
```

The result of the Groovy script is this component for the dashboard:

![Advanced Box](assets/images/dashboard-on-the-fly/dashboard-on-the-fly-box-groovy.png)