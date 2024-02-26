---
layout: single
permalink: /dashboards-advanced
last_modified_at: 2022-08-07
toc: true
sidebar:
  nav: "docs"
---

# Advanced Dashboards

The platform provides a mechanim to extend a dashboard by implementing customized dashboards group builders.

## `DashboardGroupBuilder` interfaces

To begin creating a customizable dashboard, for organizational purposes, create a folder called "dashboard" in your project. Inside this folder, you will create a class with a name that reflects what will be implemented. In the example below, a component was created to add boxes with information about a Travel Plan process.

![File](assets/images/dashboard-advanced/pasta-dashboard.png)

The DashboardGroupBuilder is an abstract class containing an abstract method, <b>buildGroup</b>, without implementation. To create a customizable dashboard component, it is necessary to extend the one of the Dashboard classes the <b>DashboardBoxGroupBuilder</b> or the <b>DashboardCardGroupBuilder</b>and implement this method and providing parameters from the <b>DashboardRequestModel</b> class for the Dashboard model, and a groupConfig from the <b>DashboardGroupConfigDTO</b> class, which will be used for assembling the boxes, charts, and tables.

Here is an example of the beginning of creating a TravelPlan process boxes component for the dashboard.

```java
@Service
public class TravelPlanDashboardBoxGroupBuilder extends DashboardBoxGroupBuilder {

  public TravelPlanDashboardBoxGroupBuilder() {

  }

  @Override
  public BoxGroupModel buildGroup(DashboardRequestModel dashboardRequestModel, DashboardGroupConfigDTO dashboardGroupConfigDTO) {
    return null;
  }
}
```

### `DashboardBoxGroupBuilder` interface

To create a component that uses <b>boxes</b>, it is necessary to extend the <b>DashboardBoxGroupBuilder</b> class, thus implementing the buildGroup method, which will grant access to the definition of a <b>BoxGroupModel.</b>

Initially, we define a new <b>boxGroupModel</b> already specifying the title of the card containing the boxes, to facilitate customization, this title will come directly from the <b>groupConfig</b>, where the title will be defined as shown in the <b>Examples</b> section.

```java
 BoxGroupModel boxGroupModel = new BoxGroupModel().title(groupConfig.getTitle());
```

After creating the boxGroupModel we can start creating each of the boxes as shown in the examples below:

```java
    List<TravelPlan> travelPlanInstances = travelPlanRepository.findAll();
        
    boxGroupModel.addBox(new BoxModel().title("Total trips").variant("primary").value(String.valueOf(travelPlanInstances.size())));
```

This example is a bit more complex than the previous one, but basically it serves to calculate the total number of travel days in relation to all travel instances.

```java
    List<Duration> totalDuration = travelPlanInstances
                .stream()
                .map(
                    travelPlanInstance -> {
                        return Duration.between(
                            travelPlanInstance.getStartDate().atStartOfDay(),
                            travelPlanInstance.getEndDate().atStartOfDay()
                        );
                    }
                )
                .collect(Collectors.toList());
    
            Duration travelTotalDuration = totalDuration.stream().reduce(Duration.ZERO, Duration::plus);
    
            boxGroupModel.addBox(
                new BoxModel().title("Total days traveled").variant("secondary").value(String.valueOf(travelTotalDuration.toDays()))
            );
```

And finally, we just need to <b>return the boxGroupModel</b>.

This is the result:

![Result boxes](assets/images/dashboard-advanced/dashboard-advanced-box.png)

### `DashboardChartGroupBuilder` interface

To create a component that uses table, <b>bar chart and pie chart</b>, it is necessary to extend the <b>DashboardCardGroupBuilder</b> class, thus implementing the buildGroup method, which will grant access to the definition of a <b>CardGroupModel</b>.

```java
 CardGroupModel cardGroupModel = new CardGroupModel().title(groupConfig.getTitle());
```

After creating the cardGroupModel we can start creating the table and charts as shown in the examples below:

```java
    cardGroupModel.getCards().add(buildCardModelTravelPlan(travelPlanInstances));
        return cardGroupModel;
```

Here, the getCards() method is called, adding the information to be displayed in the table, bar chart, and pie chart. The buildCardModelTravelPlan method will be shown and explained below.

```java
  private CardModel buildCardModelTravelPlan(List<TravelPlan> travelPlanInstances){

        CardModel card = new CardModel().title("Travel Plan Chart");

        card.getTableModel().addHead("Travel Country").addHead("Trips");

        Map<String, Long> countryCounts = travelPlanInstances.stream()
            .collect(Collectors.groupingBy(TravelPlan::getName, Collectors.counting()));

        for (String countryName : countryCounts.keySet()) {
          TableRowModel tableRow = new TableRowModel();
            if (countryName == null) {
                tableRow.setTitle("No Travel");
            } else {
                tableRow.setTitle(countryName);
            }
            tableRow.addValue(new BigDecimal(countryCounts.getOrDefault(countryName, 0L)));
            card.getTableModel().addRow(tableRow);
        }

        return card;
}
```

In this method, initially, a list is passed which I want to use as a basis for assembling my information. In this example, I'm using the list of instances of the <b>Travel Plan process</b>.

Firstly, a new CardModel is defined, providing a <b>title for the card</b>. Then, the columns of the table are defined. In this setup, it was decided to build the table and the charts with the names of the countries and the quantity of trips made to those countries. Then, a Map of String and Long is constructed to ensure that the country and the number of trips are not repeated. After that, the table is assembled properly through this loop, <b>defining each row of the table</b> and adding it to the card.

![Dashboard card](assets/images/dashboard-advanced/dashboard-advanced-chart.png)

![Dashboard table](assets/images/dashboard-advanced/dashboard-advanced-chart-table.png)

![Dashboard bar chart](assets/images/dashboard-advanced/dashboard-advanced-bar-chart.png)

![Dashboard pie chart](assets/images/dashboard-advanced/dashboard-advanced-pie-chart.png)

## Examples

To use your customizable dashboard component, you will access it in your project:

Access the Administration tab, click on Process Definitions, choose the process you want to apply the customizable dashboard to, and click on <b>Dashboard</b>.

![Dashboard button](assets/images/dashboard-advanced/dashboard-process-definition.png)

On the process Dashboard page, you should click on <b>Config</b>.

![Dashboard config](assets/images/dashboard-advanced/dashboard-advanced-config.png)

In the process Dashboard configuration, by clicking on the <b>Add Group button</b>, you can add a new component to the Dashboard. First, we define the name that will be given to the component's card and <b>saved in groupConfig</b>, as commented in <b>DashboardBoxGroupBuilder</b>. After that, we select the Group Builder that will contain the name given to the dashboard component class, where <b>the first letter should be lowercase</b>.

We can also change the order in which each component will be presented by clicking on <b>the arrows to the top right of the card</b>.

![Dashboard add group](assets/images/dashboard-advanced/dashboard-advanced-add-component.png)




