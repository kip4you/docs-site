---
layout: single
permalink: /subprocess
last_modified_at: 2022-10-28
toc: true
sidebar:
    nav: "docs"
---

# Subprocess

## Working with Subprocess
A sub-process is a means of entering a flow of an alternate process during the execution of the main process.\
To better understand how the creation of a subprocess is performed, the example of a quotation application will be used.

## Camunda Configuration

The first thing we will do is create a task and define it as a sub-process by selecting
**Call Activity** and **Parallel Multi-Instance** as shown in the red underline in the image below:

![Task Configure Subprocess](assets/images/subprocess/taskConfigure_subprocess.png)

After the task created, you must define a name and id in **General**, in the **multi-instance** tab we will inform that the subprocess will receive a **Collection** of elements called *quotationProcesses*,
referring to a List containing all the suppliers available to quotation and in **Element Variable** will be set
to the name of *quotationProcess* that refers to each instance of quotationProcesses.

![Subprocess properties Configure ](assets/images/subprocess/TaskSubprocessProperties_configure.png){:style="display:block; margin-left:auto; margin-right:auto"}

On the **Called Element** tab, some things will be defined such as:

**Type**: BPMN
\
**Called Element**: quotationProcess

Also select the **Bussines Key** checkbox with this the **Bussines Key Expression**
field will be enabled where we will define **#{quotationProcess.getQuotation().number}** this being the business key created for the quote.

![Subprocess properties Configure Called Element](assets/images/subprocess/TaskSubprocessProperties_configureCalledElement.png){:style="display:block; margin-left:auto; margin-right:auto"}

Then create a Service Task with the name *Create Quotation Processes* 
in the **Delegate Expression** tab, insert this name *requestForQuotationProcessTaskCreateQuotationProcessesDelegate*.

![Service Task Create Quotation Processes](assets/images/subprocess/ServiceTaskCreateQuotationProcesses.png){:style="display:block; margin-left:auto; margin-right:auto"}

Finally, inside the BPMN of the subprocess, create a Service Task with the name of *Setup Subprocess* and in the **implementation** tab define:

**Type**: Delegate Expression
\
**Delegate Expression**: quotationProcessTaskSetupProcessDelegate

![Setup SubProcess Task Configure](assets/images/subprocess/SetupSubprocesssTaskConfigure.png){:style="display:block; margin-left:auto; margin-right:auto"}

## Backend Configuration

After preparing all the necessary tasks in camunda we will make some changes to the generated code, create a **Java Delegate** class with the name *quotationProcessVarMappingDelegate* that implements the **DelegateVariableMapping** interface,
this is necessary because we need to change the **ProcessEntity** reference from **RequestForQuotationProcess** to **QuotationProcess**,
when this exchange of reference is performed on the **ProcessEntity**,
the **QuotationProcess** also receives a reference to **RequestForQuotationProcess** so that the reference of the previous process is not lost.

```java
@Component
public class QuotationProcessVarMappingDelegate implements DelegateVariableMapping {

    @Override
    public void mapInputVariables(DelegateExecution delegateExecution, VariableMap variableMap) {
        variableMap.putValue(
            RequestForQuotationProcessConstants.REQUEST_FOR_QUOTATION_PROCESS,
            delegateExecution.getVariable(CamundaConstants.PROCESS_ENTITY)
        );
        variableMap.putValue(CamundaConstants.PROCESS_ENTITY, delegateExecution.getVariable(QuotationProcessConstants.QUOTATION_PROCESS));
    }

    @Override
    public void mapOutputVariables(DelegateExecution delegateExecution, VariableScope variableScope) {}
}
```

Create a **Java Delegate** interface with the name of *requestForQuotationProcessTaskCreateQuotationProcessesDelegate* implementing **JavaDelegate**,
being responsible for preparing our list of subprocesses and instantiating the quotationProcess information for the subprocess.

```java
@Component
public class RequestForQuotationProcessTaskCreateQuotationProcessesDelegate implements JavaDelegate {

   @Autowired
   private RequestForQuotationProcessRepository requestForQuotationProcessRepository;

   @Autowired
   private RequestForQuotationRepository requestForQuotationRepository;

   @Autowired
   private ProviderMapper providerMapper;

   @Autowired
   private QuotationProcessMapper quotationProcessMapper;

   @Autowired
   private QuotationProcessRepository quotationProcessRepository;

   @Override
   public void execute(DelegateExecution delegateExecution) throws Exception {
       RequestForQuotationProcessDTO requestForQuotationProcessDTO = (RequestForQuotationProcessDTO) delegateExecution.getVariable(
           CamundaConstants.PROCESS_ENTITY
       );
       RequestForQuotationProcess requestForQuotationProcess = requestForQuotationProcessRepository
           .findById(requestForQuotationProcessDTO.getId())
           .orElseThrow();
       updatedRequestForQuotationStatus(requestForQuotationProcess.getRequestForQuotation());
       List<QuotationProcessDTO> quotationProcesses = createQuotationProcesses(
           (List<ProviderDTO>) delegateExecution.getVariable(RequestForQuotationProcessConstants.PROVIDERS),
           requestForQuotationProcess
       );
       delegateExecution.setVariable(RequestForQuotationProcessConstants.QUOTATION_PROCESSES, quotationProcesses);
   }

   private void updatedRequestForQuotationStatus(RequestForQuotation requestForQuotation) {
       requestForQuotationRepository.updateStatusById(StatusRFQ.QUOTING, requestForQuotation.getId());
   }

   private List<QuotationProcessDTO> createQuotationProcesses(
       List<ProviderDTO> providers,
       RequestForQuotationProcess requestForQuotationProcess
   ) {
       List<QuotationProcessDTO> quotationProcesses = new ArrayList<>();
       int index = 1;
       for (ProviderDTO provider : providers) {
           quotationProcesses.add(createQuotationProcess(requestForQuotationProcess, providerMapper.toEntity(provider), index++));
       }
       return quotationProcesses;
   }

   private QuotationProcessDTO createQuotationProcess(
       RequestForQuotationProcess requestForQuotationProcess,
       Provider provider,
       int index
   ) {
       QuotationProcess quotationProcess = new QuotationProcess();
       quotationProcess.setQuotation(new Quotation());
       quotationProcess.getQuotation().setRequestForQuotation(requestForQuotationProcess.getRequestForQuotation());
       quotationProcess.getQuotation().setStatusQuotation(StatusQuotation.QUOTING);
       quotationProcess.getQuotation().setProvider(provider);
       quotationProcess.getQuotation().setItem(requestForQuotationProcess.getRequestForQuotation().getItem());
       quotationProcess.getQuotation().setNumber(requestForQuotationProcess.getRequestForQuotation().getNumber() + "." + index);
       return quotationProcessMapper.toDto(quotationProcessRepository.save(quotationProcess));
   }
}

```

After that create a **Java Delegate** class with the name *QuotationProcessTaskSetupProcessDelegate* that implements the **JavaDelegate** interface,
this part is necessary to instantiate the **ProcessInstance** so that there are no problems when executing the subprocess.

```java
@Component
public class QuotationProcessTaskSetupProcessDelegate implements JavaDelegate {

   @Autowired
   private ProcessDefinitionRepository processDefinitionRepository;

   @Autowired 
   private ProcessDeploymentRepository processDeploymentRepository;

   @Autowired
   private ProcessInstanceRepository processInstanceRepository;

   @Autowired
   private QuotationProcessRepository quotationProcessRepository;

   @Autowired
   private RuntimeService runtimeService;

   @Autowired
   private QuotationProcessMapper quotationProcessMapper;

   @Override
   public void execute(DelegateExecution delegateExecution) throws Exception {
       QuotationProcessDTO quotationProcessDTO = (QuotationProcessDTO) delegateExecution.getVariable(CamundaConstants.PROCESS_ENTITY);
       ProcessDefinition processDefinition = processDefinitionRepository
           .findByBpmnProcessDefinitionId(QuotationProcessConstants.QUOTATION_PROCESS_BPMN_ID)
           .orElseThrow();
       ProcessDeployment processDeployment = processDeploymentRepository
           .findByProcessDefinitionIdAndStatusIsActiveAndTenantIsNull(processDefinition.getId())
           .orElseThrow();
       ProcessInstance processInstance = new ProcessInstance();
       processInstance.setProcessDefinition(processDefinition);
       processInstance.setCamundaProcessDefinitionId(processDeployment.getCamundaProcessDefinitionId());
       processInstance.setCamundaDeploymentId(processDeployment.getCamundaDeploymentId());
       processInstance.setProps(processDeployment.getProps());
       processInstance.setStartDate(LocalDateTime.now());
       processInstance.setUsername(SecurityUtils.getCurrentUserLogin().orElseThrow());
       processInstance.setStatus(StatusProcessInstance.RUNNING);
       processInstance.setBusinessKey(delegateExecution.getBusinessKey());
       processInstance.setCamundaProcessInstanceId(delegateExecution.getProcessInstanceId());
       ProcessInstance processInstanceSaved = processInstanceRepository.save(processInstance);
       QuotationProcess quotationProcess = quotationProcessRepository.findById(quotationProcessDTO.getId()).orElseThrow();
       quotationProcess.setProcessInstance(processInstanceSaved);
       runtimeService.setVariable(
           quotationProcess.getProcessInstance().getCamundaProcessInstanceId(),
           CamundaConstants.PROCESS_ENTITY,
           quotationProcessMapper.toDto(quotationProcess)
       );
   }
}
```

Congratulations, you’ve just create a subprocess!