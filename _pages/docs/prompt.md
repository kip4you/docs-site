---
layout: single
permalink: /akip-prompt-configuration
last_modified_at: 2024-03-05
toc: true
sidebar:
  nav: "docs"
---

### Akip Prompt Configuration

The Akip Prompt Configuration is a fresh addition seamlessly integrated with ChatGPT, aimed at **facilitating the creation of process emails with ease and creativity and other texts**.

To access the Akip Prompt Configuration settings, you need to have an **Admin profile**. Once you have access, navigate to the Administration tab, where you'll find the **Prompt Configuration option**.

### Prompt Configurations

When accessing the page, the first thing we see are the prompt configurations. By default, there are some predefined configurations such as Email Problem PO, Improve, Translate, and several others, as displayed on the page below.

![Prompt Configurations](assets/images/prompt/prompt-configurations.png)

#### How to create?

To create a prompt configuration, in the upper right corner, we have a button to create one. Upon opening the page, we fill in some information. These include the **Name of the Prompt Configuration (the only mandatory field)**, the **Model** which represents the version of **GPT, Temperature, Top P, Max Tokens, Presence Penalty, Frequency Penalty**.

![Prompt Configurations create](assets/images/prompt/prompt-configuration-create-prompt.png)

And the fields that make the most difference for the text result: params, where we define Name, Label, Type, Default Value, and Values, specifying the subject to be addressed. **We can create as many parameters as we want**. Finally, we have the **Messages** section where we **instruct** the artificial intelligence on **what to do with the created parameter** and what action to take with that information. **We can also create multiple messages**.

![Prompt Configurations params and messages](assets/images/prompt/prompt-configuration-create-params-messages.png)

After configuring, you just need to click **"Save"** and it will be listed on the prompt configurations page.

#### How to use?

Certainly, to utilize this created prompt configuration, in the BPMN of the process you developed, you can define in which task you want to display this text area integrated with ChatGPT. Let's demonstrate with a simple BPMN:

A BPMN diagram was then created with a start event, a user task, and an end event, where we will **integrate our text area field with ChatGPT in this user task**.

![Prompt Configurations simple BPMN](assets/images/prompt/prompt-simple-bpmn.png)

After creating the BPMN, when clicking on the User Task Prompt Config Test, we will go to the **Forms** section and add a form field. In this form field, we will give it a **suggestive ID using lowercase and camel case**, then in **Type**, we will choose the **custom type**, adding precisely **AkipTextareaChatGptField** to recognize the text area with ChatGpt integration and a label to display on the page.

![Prompt Configurations BPMN configuration 1](assets/images/prompt/prompt-configuration-form-chat.png)

With the form field configuration set, the next step is to decide which Akip prompt configurations we will use in this text area integrated with ChatGPT. To do this, we navigate to the **Properties** and add the ID called **promptConfigurations**. In the Value field, we need to add the **names of the Akip prompt configurations that we want to utilize followed by commas**.

![Prompt Configurations BPMN configuration 2](assets/images/prompt/prompt-configuration-properties.png)

Upon deploying this process, we can visualize the text area that we defined in the Prompt Config Test task.

![Prompt Configurations - practical example](assets/images/prompt/prompt-configuration-real-example.png)

### Sandbox Area

The Sandbox Area is a space below the prompt configurations where you can test some of the prompt configurations created previously. In the first part of this space, we can simply test a **text area field with anything we want to write**. Then, in the top right of the text area, after you write, you can find and uses a button with options like **"Improve" (to enhance the text written)** and a **"Translate"** option that contains some of the languages defined in the prompt configuration of the Translate.

![Prompt Configurations Sandbox](assets/images/prompt/prompt-configuration-sandbox-area.png)

#### Example 1

If you write in the text area, you can click on the button in the top right corner and use the "Improve" option, which will enhance your text. The other option is "Translate," where you select the desired language and click "Retry" to translate. After generating the text, if you click "Accept," the generated text will be displayed, replacing the old text in the text area.

![Prompt Configurations Example 1](assets/images/prompt/prompt-configuration-example-1.png)

After you click the **Accept** button:

![Prompt Configurations Example 1 result](assets/images/prompt/prompt-configuration-example-1-result.png)

#### Example 2

The other part of the Sandbox Area is an example of a purchase order with the following information: **number**, **buyer**, **seller**, and **value**. These details **can be modified in the input fields**. Additionally, there's the **task name**, which is already defined, and the **email**.

![Prompt Configurations Sandbox - Using Context](assets/images/prompt/prompt-configuration-using-context.png)

By modifying the values of the fields to the ones we want, we can click on the button in the upper right corner and select the **Email Problem PO** option, thus accessing the following modal that will generate a text containing the information described in the fields with a **customized apology request** of each problem you select.

![Result Prompt Configurations Sandbox - Using Context](assets/images/prompt/prompt-configuration-example-customized-apology.png)

To generate this message, a prompt configuration was created for this Email Problem PO. On the creation screen, parameters such as **Name, Label, Type, Default Value, and Values** were defined, along with a list of possible issues to be selected during text generation. Additionally, **messages to be used for constructing the customized text** generated by artificial intelligence were described.

![Prompt Configurations Params](assets/images/prompt/prompt-configuration-params.png)

![Prompt Configurations Messages](assets/images/prompt/prompt-configuration-messages.png)