---
layout: single
permalink: /timeline
last_modified_at: 2024-02-19
toc: true
sidebar:
nav: "docs"
---

# Timeline

## O que é a Timeline?

A timeline é uma recurso que visa facilitar a visualização de um processo como um todo, permitindo assim usuários com menos conhecimento em BPNM poderem entender o andamento do processo de maneira linear, acompanhando a tarefa que está em andamento, as finalizadas e as tarefas que faltam finalizar.

## Como utilizar a timeline?

### 1. Acessando a timeline de um processo

Para podermos configurar a timeline, precisamos primeiro decidir qual o processo e acessar a listagem e configuração, através da tela de Process Definitions no botão timelines.

<b>POR FOTO DA PROCESS DEFINITION MOSTRANDO O BOTÃO TIMELINES</b>

### 2. Timelines

Ao acessar o botão somos levados para uma página em que são listadas informações das timelines criadas para aquele processo, podendo visualizar, editar e excluir uma determinada timeline. Caso queira configurar uma nova timeline, clicamos no botão "Create a new timeline".

<b> POR FOTO DA TELA EM GERAL</b>

<b> TELA DE VISUALIZAR </b>

<b> TELA DE EDITAR </b>

<b> TELA DE EXCLUIR </b>

<b> MOSTRAR BOTÃO PARA CONFIGURAR TIMELINE </b>

### 3. Criação de uma nova timeline

Na página de criação da timeline devemos dar foco para algumas informações que constam na tela.

Primeiramente no canto direito da página podemos visualizar as Tasks Definition Keys, ou seja estes são todos os IDs de tarefas que estão inclusas em seu BPMN, podendo também utilizar o botão para copiar o nome dela, para uso que vou comentar logo adiante.

<b> POR FOTO DANDO FOCO PARA OS TASK DEFINITION KEY</b>

Abaixo da listagem de Task Definition Key temos alguns exemplos de expressões que poderemos montar nossa timeline, sendo assim temos diferentes maneiras de representar um passo na timeline podendo por exemplo ser somente uma tarefa como foco para aquele passo, ou tarefas com condicinais "AND" e "OR", podendo utilizar de parênteses para inclusão de mais de uma task. Dessa maneira podemos resumir e simplificar o entendimento de um processo que seria complexo em algo de agradável visualização.

<b> POR FOTO DOS EXEMPLOS QUE TEM NA PÁGINA OU MONTAR UNS EXEMPLOS DE EXPRESSÕES </b>

Seguindo para criação da timeline temos dois campos iniciais que a primeira que é o Timeline Name, como o nome diz informamos um nome sugestivo para a timeline e o segundo campo é o Timeline Condition, neste campo botamos uma expressão que determinará outros fluxos de tarefas que queremos seguir na timeline. Como a visualização da timeline é linear temos que definir estes outros fluxos para que quando determinada Timeline Condition seja atendida a visualização mude para atender a determinado fluxo.

<b> TENTAR POR UMA IMAGEM DEMONSTRANDO </b>

<b> É importante lembrar que a primeira timeline não precisará incluir um Timeline Condition já que nela será definido um fluxo default para o processo. </b>

<b> por a criação de uma timeline default e uma com conditions </b>


