---
title: Guia de início rápido do Workday
description: Um guia de início rápido para clientes que desejam usar o Adobe Sign em seus ambientes Workday.
uuid: 10bf8ee8-9075-44d1-a836-e454950e2d9a
products: Adobe Sign
content-type: reference
discoiquuid: 13135c88-4c39-4707-b7ba-63ff94769258
locnotes: All languages; screenshots to follow what's there already (seems there is a mix within a given language version of the article)
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 8b6fa8b4-e240-4ebe-ae2a-8807d75a6c69
source-git-commit: 2cc0ea55ee7dca3682896c61c85eec29a555339c
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 0%

---

# [!DNL Workday] Guia de início rápido{#workday-quick-start-guide}

[**Entre em contato com o Suporte da Adobe Sign**](https://www.adobe.com/go/adobesign-support-center)

## Visão geral {#overview}

Este documento foi criado para ajudar [!DNL Workday] os administradores entendem como personalizar o [!DNL Workday] Processos corporativos para incluir o Adobe Sign na obtenção de assinaturas eletrônicas. Para usar o Adobe Sign em [!DNL Workday], você deve saber como criar e modificar [!DNL Workday] itens como:

* [!UICONTROL Estrutura de Processo de Negócios]
* Instalação e configuração de inquilino
* Relatórios e [!DNL Workday] Integração com o Studio

## Acessar o Adobe Sign em [!DNL Workday] {#access-adobe-sign}

[!UICONTROL Recurso de assinatura eletrônica do Adobe Sign] é apresentado como [!UICONTROL Etapa Revisão do documento] ação no âmbito do [!UICONTROL Estrutura de processos de negócios (BPF)] e como uma tarefa Distribuir documentos.

## [!UICONTROL Etapa Revisão do documento] {#review-document-step}

Adobe Sign para [!DNL Workday] é exposta através da [!UICONTROL Etapa Revisão do documento] que você pode adicionar a qualquer um dos mais de 400 processos de negócios [!DNL Workday], incluindo [!UICONTROL Oferta], [!UICONTROL Distribuir documentos e tarefas], [!UICONTROL Propor Compensação]e muito mais.

Você pode consultar o [[!DNL Workday] artigos comunitários sobre [!UICONTROL Etapa Revisão do documento]](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg).

Há uma relação 1:1 entre [!UICONTROL [!UICONTROL Etapa Revisão do documento]s] e faturáveis com a Adobe Sign. É possível combinar vários documentos em um só [!UICONTROL Etapa Revisão do documento] e são apresentados como um pacote único para assinatura.

**Observação**: Apenas um *Dinâmico* documento pode ser referenciado em um [!UICONTROL Etapa Revisão do documento].

Para definir uma função [!UICONTROL Etapa Revisão do documento]:

1. Inserir um [!UICONTROL Etapa Revisão do documento].
1. Especifique os Grupos (funções) que podem atuar no [!UICONTROL Etapa Revisão do documento].

![As etapas do Processo de Negócios](images/insert-review-doc-steptornm-575.png)

Para configurar o [!UICONTROL Etapa Revisão do documento]:

1. Especifique o *[!UICONTROL Tipo de integração de assinatura eletrônica]* como *[!UICONTROL eSign da Adobe]*.

1. Adicione linhas à Grade de assinatura.

   * A grade de assinatura especifica a ordem de série na qual o documento é roteado para assinatura. Cada linha pode conter uma ou mais funções e cada linha representa uma etapa no processo de assinatura.
   * Cada membro da função em uma etapa específica é notificado de que um evento de assinatura está pendente.
   * Depois que uma única pessoa da função assina, a etapa da linha é concluída e o documento é movido para a próxima etapa da linha.
   * Quando todas as linhas tiverem sido assinadas, o [!UICONTROL Etapa Revisão do documento] está concluído.

1. Especifique o documento a ser assinado. Se o documento for um [!UICONTROL Oferta BP], você pode usá-lo a partir de uma etapa Gerar documento. Caso contrário, escolha um documento ou relatório existente.

1. Repita a etapa 3 para quantos documentos forem necessários.

   ![Configurar Etapa de Revisão de Documento](images/configure-rd-stepsmaller-575.png)

1. Opcionalmente, adicione um &quot;usuário de redirecionamento&quot; para capturar as ações de &quot;recusar assinatura&quot;. Quando os usuários recusam, [!DNL Workday] roteia novamente os documentos para um grupo de segurança configurado para revisão.

No menu de ações relacionadas de um [!UICONTROL Etapa Revisão do documento], selecione **[!UICONTROL Processo de negócios]** > **[!UICONTROL Manter Redirecionamento]**. Em seguida, selecione uma das seguintes opções:

* **[!UICONTROL Enviar de volta]**: Para permitir que os membros do grupo de segurança enviem uma etapa de volta a uma etapa anterior no processo de negócios. O processo de negócios é reiniciado a partir dessa etapa.
* **[!UICONTROL Mover para a próxima etapa]**: Para permitir que os membros do grupo de segurança encaminhem uma etapa para a próxima etapa do processo de negócios.
* **[!UICONTROL Grupos de Segurança]**: Para redirecionar etapas no fluxo do processo empresarial. Os grupos de segurança exibidos nesse prompt são selecionados na política de segurança do processo de negócios na seção Redirecionar.

## Notas da etapa do processo empresarial {#business-process-step-notes}

O [!UICONTROL Estrutura de Processo de Negócios] é poderoso; no entanto, você deve garantir que:

* Todo Processo de Negócios deve ter uma etapa de conclusão, que é idealmente o final do processo de negócios.

* Uma etapa de conclusão é definida no menu de ações relacionadas do ícone de pesquisa. Isso é possível apenas ao &quot;visualizar&quot; o BP e não ao &quot;editá-lo&quot;.

* Cada etapa do processo de negócios é executada sequencialmente.

   Você pode alterar a ordem de uma etapa alterando o valor da ordem. Por exemplo, para inserir uma etapa entre os itens &quot;c&quot; e &quot;d&quot;, especifique um novo item como &quot;ca&quot;.

### Exemplo: oferta {#example-offer}

O BP da oferta é um subprocesso do [!UICONTROL BP Dinâmico de Aplicativo de Trabalho] que deve ser configurado para executar o BP da Oferta. É acionado quando o estado do Aplicativo de trabalho é movido para &quot;[!UICONTROL Oferta]&quot; ou &quot;[!UICONTROL Fazer Oferta]&quot;.

No exemplo abaixo, uma [!UICONTROL Etapa Revisão do documento] O está usando uma etapa de Documento dinâmico para a América do Norte e o Japão.

![Exemplo de um [!DNL Workday] Processo de negócios](images/bp-for-offersmaller-575.png)

Este BP faz o seguinte:

* Solicita ao promotor da BP que proponha uma compensação para o candidato (etapa b).
* Usa uma condição de etapa para testar se o país atual NÃO é o Japão.

   Se verdadeiro, executa a etapa &quot;ba&quot;, que usa um documento em inglês.

   Se falso, executa a etapa &quot;bb&quot;, que usa um documento em japonês.

* Define o processo de assinatura no [!UICONTROL Etapa Revisão do documento] &quot;bc&quot;.
* Define o ponto de decisão para fazer uma oferta na etapa de conclusão obrigatória &quot;d&quot;.

O documento dinâmico que está sendo gerado na etapa &quot;ba&quot; é chamado [!UICONTROL Carta de oferta] e contém um único bloco de texto chamado [!UICONTROL Oferta rápida]. Você pode adicionar vários blocos de texto, como cabeçalho, saudação, remuneração, estoque, fechamento, termos e muito mais, conforme necessário.

![[!DNL Workday] exibir página do documento](images/offer-letter-575.png)

A carta de oferta dinâmica abaixo é criada no [!DNL Workday] editor de rich text. Os itens destacados em *cinza* são [!DNL Workday] objetos fornecidos que fazem referência a dados contextuais.

Itens em {{brackets}} são [Tags de texto Adobe](https://adobe.com/go/adobesign_text_tag_guide).

![Exemplo de formulário dinâmico](images/script.png)

No âmbito do [!UICONTROL Etapa Revisão do documento], o documento dinâmico é referenciado da etapa anterior e define o processo de assinatura sequencial por meio de dois grupos de assinatura.

O comportamento ilustrado abaixo roteia o documento gerado dinamicamente primeiro para o Gerente de Contratação e, em seguida, para o Candidato.

![[!DNL Workday] grupos de assinatura sendo definidos](images/configure-rd-stepsmaller-575.png)

### Exemplo: Distribuir documentos {#example-distribute-documents}

Introduzido em [!DNL Workday] 30, a tarefa Distribuir documentos ou tarefas em massa pode ser usada para enviar um único documento para um grande grupo (&lt;20K) de signatários individuais. É limitado a uma única assinatura por documento. A criação de uma distribuição é feita acessando o[!UICONTROL Criar e distribuir documentos ou tarefas]da barra de pesquisa.

Exemplo: Enviar um formulário de escolha de patrimônio líquido do funcionário para todos os gerentes com [!UICONTROL Serviços modernos globais]. Você pode filtrá-lo ainda mais para gerentes individuais, se desejar.

Você também pode acessar o **Exibir Distribuir Documentos ou Tarefas** para acompanhar o progresso da distribuição.

![](images/create-distributedocumentsortasks.png)

### Exemplo: Relatórios {#example-reporting}

[!DNL Workday] A tem uma infraestrutura de emissão de relatórios avançada. Para ver os detalhes do processo do Adobe Sign, inspecione os elementos do *Evento de Revisão de Documento*.

Veja abaixo um relatório personalizado simples que pode ser executado em todos os BPs que procuram por transações do Adobe Sign e seus status.

![Exemplo de um [!DNL Workday] Relatório Personalizado](images/review-document-eventsmaller-575.png)

O relatório a seguir foi gerado ao examinar os BPs de oferta, integração e proposta de compensação em um locatário de implementação.

Você pode ver:

* Os documentos enviados para assinatura
* A etapa BP associada
* A próxima pessoa aguardando assinatura

![Exemplo de um [!DNL Workday] Relatar usando três objetos](images/workday-reportsmaller-575.png)

## Documentos assinados {#signed-documents}

O [!DNL Workday] o ciclo de assinatura suprime todas as notificações por email do Adobe Sign. Os usuários são informados de ações pendentes em seus [!DNL Workday] caixa de entrada.

Depois que um documento é assinado por todos os Grupos de assinatura, uma cópia do documento assinado é distribuída a todos os membros do Grupo de assinatura por email.

Para suprimir esse comportamento, entre em contato com o [!UICONTROL Adobe Sign Success Manager] ou [Equipe de suporte da Adobe Sign](https://adobe.com/go/adobesign-support-center).

No [!DNL Workday], você pode acessar os documentos assinados no registro completo do processo. Você pode encontrar:

* Documentos do trabalhador no Perfil do trabalhador e
* Documentos do candidato (cartas de oferta) no Perfil do candidato.

A imagem abaixo mostra uma carta de oferta assinada para o candidato Chris Foxx.

![Exemplo [!DNL Workday] carta de oferta](images/offer.png)

## Suporte {#support}

### [!DNL Workday] suporte {#workday-support}

[!DNL Workday] é o proprietário da integração e deve ser seu primeiro ponto de contato para perguntas sobre o escopo da integração, solicitações de recursos ou problemas na função diária da integração.

O [!DNL Workday] a comunidade tem vários bons artigos sobre como solucionar problemas de integração e gerar documentos:

* [Solução de problemas de integrações de eSignature](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [Etapa Revisão de documentos](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)
* [Geração dinâmica de documentos](https://community.workday.com/node/176443)
* [Dicas de configuração de geração de documento de oferta](https://community.workday.com/node/183242)

### Suporte ao Adobe Sign {#adobe-sign-support}

O Adobe Sign é o parceiro de integração e deve ser contatado se a integração não conseguir obter assinaturas ou se a notificação de assinaturas pendentes falhar.

Os clientes da Adobe Sign devem entrar em contato com [!UICONTROL Gerente de sucesso do cliente] para obter suporte. Em alternativa, [!UICONTROL Suporte técnico Adobe] pode ser contatado por telefone: 1-866-318-4100, aguarde a lista de produtos e digite: 4 e depois 2 (conforme solicitado).

* [Adição de tags de texto Adobe aos documentos](https://www.adobe.com/go/adobesign_text_tag_guide)

<!--
[Download PDF](images/adobe-sign-for-workday-quick-start-guide-2016.pdf)
-->
