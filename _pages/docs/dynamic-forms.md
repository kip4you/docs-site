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

For the form fields we have some types to choose from, but new types will still be added, to change between them, click in the field where you want and select type

#### String

![String Type](assets/images/dynamic-forms/types.png)

This configuration field is the same as shown in the previous section and appears as follows on the page:

![Page String](assets/images/dynamic-forms/type_string.png)

#### Long

This field type looks similar to the previous one, but as the name suggests this field is used for numbers, below we can see what it looks like:

![Page Long](assets/images/dynamic-forms/type_long.png)

#### Boolean

The boolean field type doesn't have any secrets, when you select it this will display a switch to choose the value of the field between true or false, as you can see bellow:

![Page Boolean](assets/images/dynamic-forms/type_boolean.png)

#### Date

This field type as the name suggests will display a date picker field to choose a date and this is what it looks like:

![Page Date](assets/images/dynamic-forms/type_date.png)

#### Enum

The configuration of the enum type is a little different and is displayed differently as well, first we will show the configuration and what can be done with it.

![Type Enum](assets/images/dynamic-forms/type_enum.png)

Here we have some additional fields to configure, you can add as many values ​​as you want to the enum, just click on the "+" on the right side of Add Value.

After that, just fill in the id field and the name field, the id field being the name of the variable (you will use it to reference in the code) and the name to define how the option will appear for the user.

How it would look on the page:

![Page Enum](assets/images/dynamic-forms/page_enum.png)

Remember that if you are going to do some verification on a gateway or **if you are going to use these values in some expression use the id**

#### Custom Type

The Custom Type for now has three types available, one for attachments, one for notes and other for text area field, let's take a look at them 

#### Akip Notes in start form

This type is a field where it is possible to enter notes separately, first let's take a look at the configuration

If you use the Akip Notes in the start form, you need to keep the property field without scope defined, this is because at the moment you start a process the init **does not have the process instance** created. When you initiate the start form, a **temporary process instance** is created to store any attachments or notes you insert for the next tasks, of course, if you choose to do so.

![Type Akip Notes](assets/images/dynamic-forms/type_akip_notes.png)

To work you have to insert "AkipNotesField" in the field that will appear below the custom type, otherwise it's just the configuration seen previously

How it will look on the page:

![Page Akip Notes 1](assets/images/dynamic-forms/page_akip_notes_1.png)
![Page Akip Notes 2](assets/images/dynamic-forms/page_akip_notes_2.png)
![Page Akip Notes 2](assets/images/dynamic-forms/page_akip_notes_3.png)

###### In Tasks
In the other hand if you use in tasks after the start form you need to specify in the property section the scope with **ProcessInstance** and the name that you will call it in the custom type is **AkipNotesTaskInstanceField**.

![Page Akip Notes name](assets/images/dynamic-forms/akip-notes-task-instance.png)

![Page Akip Notes processInstance](assets/images/dynamic-forms/processInstanceAkipNote.png)

The "Type" area I will explain later in the *properties* section

#### Akip Attachments in start form

This field works more or less like Akip Notes with the difference that they are not notes but attachments, let's see the configuration

If you use the Akip Attachments in the start form, you need to keep the property field without scope defined, this is because at the moment you start a process the init **does not have the process instance** created. When you initiate the start form, a **temporary process instance** is created to store any attachments or notes you insert for the next tasks, of course, if you choose to do so.

![Type Akip Attachments](assets/images/dynamic-forms/type_akip_attachments.png)

It is practically the same configuration as Akip Notes with the difference that instead of being AkipNotesField it is AkipAttachmentsField

How it looks on the page:

![Page Akip Attachments 1](assets/images/dynamic-forms/page_akip_attachments_1.png)

![Page Akip Attachments 2](assets/images/dynamic-forms/page_akip_attachments_2.png)

###### In Tasks
In the other hand if you use in tasks after the start form you need to specify in the property section the scope with **ProcessInstance** and the name that you will call it in the custom type is **AkipAttachmentsTaskInstanceField**..

![Page Akip Attachments name](assets/images/dynamic-forms/akip-attachments-task-instance.png)

![Page Akip Attachments processInstance](assets/images/dynamic-forms/processInstanceAkipNote.png)

###### Minio
Just remembering that here it is necessary to configure some storage of objects such as minio for example, this configuration can be seen in the specific section of attachments

#### Text Area

The Text Area field you will need to select type custom after creating a field in Form Fields section, them you will need to write "TextArea" to bring it.

This is how text area looks like using dynamic forms:

![Page Text Area](assets/images/dynamic-forms/type_text-area.png)

### Default Value

Accessing the field you want you will see an input called Default Value, this allows you to start your field in some value.

![Page Default Value](assets/images/dynamic-forms/default_value.png)
  
The Default Value can be applied to:
  - string
  - long
  - enum
  - boolean
  - date
  - TextArea

Here is an example:

![Page Default Value](assets/images/dynamic-forms/default_value_test.png)

![Page Default Value input](assets/images/dynamic-forms/default_value_input.png)


### Properties

In this section we will see 4 properties that are very important for the definition of dynamic forms

#### readonly

As the forms are not customized in the frontend or backend code, some customizations can be made by the properties, for example leaving a field read-only, which is the case of this property here

This is very useful when in a task you want the user to only see previously entered information.

This property only works for some types of fields like (if you try the property disabled for the same purpose, this is not going to work):
  - string
  - long
  - AkipNotesField
  - AkipAttachmentsField
  - TextArea

![Propertie Readonly](assets/images/dynamic-forms/propertie_readonly.png)

How it looks on the page:

![Page Readonly](assets/images/dynamic-forms/page_readonly.png)

#### disabled

Similar to the readonly property this one leaves the field disabled, to only see previous information.

It's important to say that this property only works for a few types of fields (if you use readonly for the same purpose, this is not going to work):
  - boolean
  - date
  - enum

![Page Disabled](assets/images/dynamic-forms/disabled.png)

#### noteTypes

When you have a notes field and you want only certain tasks to see those notes, you use this property

![Propertie Note Types](assets/images/dynamic-forms/propertie_noteTypes.png)

![Page Note Types](assets/images/dynamic-forms/page_noteTypes.png)

Only fields that have the noteTypes = User property will be able to see these notes, and you can add more than one type to a note field

#### attachmentTypes

It follows the same line as noteTypes, but now they are attachments that will be typed to have a control whether it will be shown or not

![Propertie Note Types](assets/images/dynamic-forms/propertie_attachmentTypes.png)

![Page Note Types](assets/images/dynamic-forms/page_attachmentTypes.png)

Only fields that have the property attachmentTypes = PostDocument will be able to see these attachments, and you can add more than one type to an attachment field