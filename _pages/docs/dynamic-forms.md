---
layout: single
permalink: /dynamic-forms
last_modified_at: 2023-08-24
toc: true
sidebar:
  nav: "docs"
---

# Dynamic forms

The dynamic forms (low-code tool) that we work on in this article are assembled and configured through the camunda tool, during this article we will use the beginning of an incident management process to exemplify the concepts

![Incident Management Process](assets/images/dynamic-forms/incident_management_process_beginning.png)

## Element Documentation

The element documentation field is basically a message or instruction that you will leave so that you are running that specific task, it will appear before the form fields

In the camunda:
![Camunda Element Documentation](assets/images/dynamic-forms/incident_management_process_element_documentation.png)
When executing the platform task:
![Page Element Documentation](assets/images/dynamic-forms/page_element_documentation.png)

## Definition of fields

The step-by-step process for creating form fields is as follows:

image for step by step reference:
![Form_fields](assets/images/dynamic-forms/form_fields.png)

- To access the field definition part, just click on the "forms" tab
- then click on the "+" icon to add a new field
- Enter the variable ID (variable name in the process)
- Select the type of variable (explained later)
- Insert the Field Label, to help the user understand which field this is
- If you want to put a default value for the field feel free

Okay, now you have a field, repeat this process to create the fields you want, but to find out more options for field types or validations and properties, keep reading the article

### Variable types

For the form fields we have some types to choose from, but new types will still be added, para alternar entre eles, clique no campo que você deseja e abra o select de type

#### String

![String Type](assets/images/dynamic-forms/types.png)

This configuration field is the same as shown in the previous section and appears as follows on the page:

![Page String](assets/images/dynamic-forms/type_string.png)