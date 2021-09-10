---
title: Guia de início rápido do Workday
description: Um guia de início rápido para clientes que desejam usar o Adobe Sign em seus ambientes Workday.
uuid: 10bf8ee8-9075-44d1-a836-e454950e2d9a
products: Adobe Sign
content-type: reference
discoiquuid: 13135c88-4c39-4707-b7ba-63ff94769258
locnotes: All languages; screenshots to follow what's there already (seems there is a mix within a given language version of the article)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 8b6fa8b4-e240-4ebe-ae2a-8807d75a6c69
source-git-commit: d462ccf41fa5483cfa02f5eaf154c23f26157a1e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Workday] Guia de início rápido{#workday-quick-start-guide}

[**Entrar em contato com o Suporte do Adobe Sign**](https://adobe.com/go/adobesign-support-center_br)

## Visão geral {#overview}

Este documento foi desenvolvido para ajudar [!DNL Workday] os administradores a entender como personalizar os [!DNL Workday] Processos corporativos para incluir a Adobe Sign para obter assinaturas eletrônicas. Para usar o Adobe Sign em [!DNL Workday], você deve saber como criar e modificar [!DNL Workday] itens como:

* Estrutura do processo de negócios
* Configuração e configuração do inquilino
* Integração com o Reporting and [!DNL Workday] Studio

## Acesso ao Adobe Sign diretamente do [!DNL Workday] {#access-adobe-sign}

O recurso de assinatura eletrônica da Adobe Sign é exibido como uma ação [!UICONTROL Revisar etapa do documento] no Business Process Framework (BPF) e como uma tarefa Distribuir documentos.

## [!UICONTROL Etapa de Review Document (Revisão de documento)] {#review-document-step}

A Adobe Sign para [!DNL Workday] é exposta pela [!UICONTROL Etapa de revisão do documento] que você pode adicionar a qualquer um dos mais de 400 processos corporativos em [!DNL Workday], incluindo Oferta, Distribuir documentos e tarefas, Propor compensação e muito mais.

Você pode consultar os [[!DNL Workday] artigos da comunidade em [!UICONTROL Etapa de revisão do documento]](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg).

Há uma relação 1:1 entre [!UICONTROL [!UICONTROL Etapa de revisão do documento]s] e transações faturáveis com a Adobe Sign. Você pode combinar vários documentos em uma única [!UICONTROL Etapa de revisão do documento] e eles são apresentados como um único pacote para assinatura.

**Nota**: Somente um único documento  ** do Dynamic pode ser referenciado em uma etapa [!UICONTROL  específica da ]revisão do documento.

Para definir uma [!UICONTROL Etapa de Revisão do Documento] funcional:

1. Insira uma [!UICONTROL Etapa de revisão do documento].
1. Especifique os Grupos (funções) que podem atuar na [!UICONTROL Etapa de revisão do documento].

![As etapas do Processo corporativo](images/insert-review-doc-steptornm-575.png)

Para configurar a [!UICONTROL Etapa de Revisão do Documento]:

1. Especifique o *[!UICONTROL eSignature Integration type]* (Tipo de integração de eSignature) como *[!UICONTROL eSign by Adobe]*.

1. Adicionar linhas à grade de assinatura.

   * A grade de assinatura especifica a ordem serial na qual o documento está roteado para assinatura. Cada linha pode conter uma ou mais funções, bem como pode representar uma etapa no processo de assinatura.
   * Cada membro da função em uma etapa específica é notificado sobre o evento de assinatura pendente.
   * Depois que uma única pessoa da função assina, a etapa da linha é concluída e o documento continua para a próxima etapa de linha.
   * Quando todas as linhas tiverem sido assinadas, a [!UICONTROL Etapa de revisão do documento] estará concluída.

1. Especifique o documento que será assinado. Se for um BP de Offer (oferta), você pode utilizar o documento da etapa Generate Document (Gerar documento). Caso contrário, escolha um documento ou relatório já existente.

1. Repita a etapa 3 para os documentos necessários.

   ![Configurar a etapa de Review Document (Revisão de documento)](images/configure-rd-stepsmaller-575.png)

1. Opcionalmente, adicione um &quot;usuário de redirecionamento&quot; para capturar ações de &quot;recusar a assinatura&quot;. Quando os usuários recusam, [!DNL Workday] redireciona os documentos para um grupo de segurança configurado para revisão.

No menu de ações relacionadas de uma [!UICONTROL Etapa de Revisão de Documento], selecione **[!UICONTROL Processo de Negócios]** > **[!UICONTROL Manter Redirecionamento]**. Em seguida, selecione uma das seguintes opções:

* **[!UICONTROL Enviar de volta]**: Para permitir que os membros do grupo de segurança enviem uma etapa de volta para uma etapa anterior no processo de negócios. O processo corporativo reinicia a partir dessa etapa.
* **[!UICONTROL Mover para a próxima etapa]**: Para permitir que os membros do grupo de segurança encaminhem uma etapa para a próxima etapa no processo de negócios.
* **[!UICONTROL Grupos]** de segurança: Para redirecionar as etapas no fluxo do processo de negócios. Os grupos de segurança exibidos nesse prompt são selecionados na política de segurança do processo de negócios na seção Redirecionar.

## Notas de etapa do processo comercial {#business-process-step-notes}

O Business Process Framework é poderoso; no entanto, você deve garantir que:

* Cada Processo de Negócios deve ter uma etapa de conclusão, que é ideal no final do processo de negócios.

* Uma etapa de conclusão é definida no menu de ações relacionadas do ícone de pesquisa. Isso só é possível ao &quot;visualizar&quot; a BP e não ao &quot;editá-la&quot;.

* Cada etapa do processo corporativo é executada de modo sequencial.

   Você pode alterar a ordem de uma etapa ao alterar o valor dela. Por exemplo, para inserir uma etapa entre os itens &quot;c&quot; e &quot;d&quot;, especifique um novo item como &quot;ca&quot;.

### Exemplo: oferta {#example-offer}

O BP da oferta é um subprocesso do BP dinâmico do aplicativo de trabalho que precisa ser configurado para executar o BP da oferta. É acionado quando o estado Candidatura a emprego é movido de “Offer” (Oferta) ou “Make Offer” (Fazer oferta).

No exemplo abaixo, uma [!UICONTROL Etapa de revisão do documento] está usando uma etapa de Documento dinâmico para a América do Norte e o Japão.

![[!DNL Workday]Exemplo de um Processo corporativo do ](images/bp-for-offersmaller-575.png)

O BP faz o seguinte:

* Solicita ao iniciador do BP que proponha uma compensação para o candidato (etapa b).
* Usa uma condição de etapa para testar se o país atual NÃO é o Japão.

   Se verdadeiro, ele executa a etapa &quot;ba&quot; que usa um documento em inglês.

   Se for falso, ele executa a etapa &quot;bb&quot; que usa um documento em japonês.

* Define o processo de assinatura na [!UICONTROL Etapa de revisão do documento] &quot;bc&quot;.
* Define o ponto de decisão para fazer uma oferta na etapa de conclusão necessária &quot;d&quot;.

O documento dinâmico gerado na etapa “ba” é chamado de [!UICONTROL Offer Letter] (Carta de proposta) e contém um único bloco de texto chamado de [!UICONTROL Rapid Offer] (Oferta rápida). Você pode adicionar vários blocos de texto, como cabeçalho, saudação, compensação, estoque, fechamento, termos e muito mais, conforme necessário.

![[!DNL Workday] exibir página do documento](images/offer-letter-575.png)

A carta de oferta dinâmica abaixo é criada no [!DNL Workday] editor de rich text. Os itens realçados em *cinza* são [!DNL Workday] objetos fornecidos que fazem referência a dados contextuais.

Os itens entre {{chaves}} são [Tags de texto da Adobe](https://adobe.com/go/adobesign_text_tag_guide_br).

![Exemplo de formulário dinâmico](images/script.png)

Na [!UICONTROL Etapa de revisão do documento], o documento dinâmico é referenciado da etapa anterior e define o processo de assinatura sequencial por meio de dois grupos de assinatura.

O comportamento ilustrado abaixo encaminhará o documento gerado dinamicamente primeiro para o Gerente de contratação e, em seguida, para o Candidato.

![[!DNL Workday] grupos de assinatura definidos](images/configure-rd-stepsmaller-575.png)

### Exemplo: Distribuir documentos {#example-distribute-documents}

Introduzida em [!DNL Workday] 30, a tarefa Distribuir Documentos ou Tarefas em Massa pode ser usada para enviar um único documento para um grande grupo (&lt;20K) de signatários individuais. É limitado a uma só assinatura por documento. A criação de uma distribuição é executada acessando a ação ‘[!UICONTROL Criar Distribuir Documentos ou Tarefas]’ na barra de pesquisa.

Exemplo: Enviar um formulário de escolha de equidade de funcionário a todos os gerentes com Global Modern Services. Você pode filtrá-lo ainda mais para gerentes individuais, se desejar.

Você também pode acessar o relatório **Exibir Distribuir Documentos ou Tarefas** para acompanhar o progresso da distribuição.

![](images/create-distributedocumentsortasks.png)

### Exemplo: relatórios {#example-reporting}

[!DNL Workday]O tem uma infraestrutura de relatórios avançados. Para analisar os detalhes do processo do Adobe Sign, inspecione os elementos do *Review Document Event* (Evento de revisão do documento).

O relatório personalizado simples abaixo pode ser executado em todos os BPs buscando as transações do Adobe Sign e seus status.

![[!DNL Workday]Exemplo de um relatório personalizado do ](images/review-document-eventsmaller-575.png)

O relatório a seguir foi gerado ao procurar por BPs de Offer (Oferta), Onboarding (Integração) e Propose Compensation (Proposta de compensação) em um inquilino de implementação.

Você pode visualizar:

* Os documentos enviados para assinatura
* A etapa BP associada
* A próxima pessoa aguardando a assinatura

![[!DNL Workday]Exemplo de um relatório do utilizando três objetos](images/workday-reportsmaller-575.png)

## Documentos assinados {#signed-documents}

O ciclo de assinatura [!DNL Workday] suprime todas as notificações por email da Adobe Sign. Os usuários são informados sobre ações pendentes na caixa de entrada [!DNL Workday].

Uma vez que um documento é assinado por todos os grupos de assinatura, uma cópia do documento assinado é distribuída para todos os membros do grupo de assinatura por email.

Para suprimir esse comportamento, você pode entrar em contato com seu Gerente de sucesso da Adobe Sign ou com a [equipe de suporte da Adobe Sign](https://adobe.com/go/adobesign-support-center).

Em [!DNL Workday], você pode acessar os documentos assinados no registro completo do processo. Você pode encontrar:

* Documentos do trabalhador no perfil do trabalhador e
* Documentos candidatos (cartas de proposta) no perfil Candidato.

A imagem abaixo mostra uma carta de oferta assinada para o candidato Chris Foxx.

![Exemplo de carta de  [!DNL Workday] oferta](images/offer.png)

## Suporte {#support}

### [!DNL Workday] apoio {#workday-support}

[!DNL Workday]O é o proprietário da integração e deve ser o seu primeiro ponto de contato em caso de dúvidas sobre o escopo da integração, solicitações de recursos ou problemas nas funções diárias da integração.

A comunidade [!DNL Workday] tem vários bons artigos sobre como solucionar problemas de integração e gerar documentos:

* [Solução de problemas de integrações de eSignature](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [Etapa Revisão de documentos](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)
* [Geração dinâmica de documentos](https://community.workday.com/node/176443)
* [Dicas de configuração de geração do documento de proposta](https://community.workday.com/node/183242)

### Suporte Adobe Sign {#adobe-sign-support}

O Adobe Sign é o parceiro da integração e deve ser contatado em caso de falha da integração ao obter assinaturas, ou em caso de falha de notificação de assinaturas pendentes.

Os clientes do Adobe Sign devem entrar em contato com o Gerenciador de sucesso do cliente (CSM) para obter suporte. Como alternativa, o Suporte técnico da Adobe pode ser contatado por telefone: 1-866-318-4100. Aguarde a lista de produtos e digite: 4, em seguida, 2 (como solicitado).

* [Adicionar tags de texto da Adobe aos documentos](https://adobe.com/go/adobesign_text_tag_guide)

<!--
[Download PDF](images/adobe-sign-for-workday-quick-start-guide-2016.pdf)
-->
