---
title: Guia do Usuário do Veeva Vault
description: Guia do usuário dos clientes da Veeva Vault sobre como usar a integração da Adobe Sign com a Veeva
products: Adobe Sign
content-type: reference
locnotes: All languages; screenshots to follow what's there already (seems there is a mix within a given language version of the article)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 39a43637-af3f-432e-a784-8f472aa86df5
source-git-commit: 63a34c2d77ba7a262670da624c86a3730de0fdc5
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 3%

---

# Adobe Sign para [!DNL Veeva Vault]: Guia do usuário {#veeva-vault-user-guide}

[**Entrar em contato com o Suporte do Adobe Sign**](https://adobe.com/go/adobesign-support-center_br)

Este documento foi desenvolvido para ajudar [!DNL Veeva Vault] os clientes a aprender a usar a Adobe Sign para [!DNL Veeva Vault] integração para enviar um contrato.

## Visão geral {#overview}

A integração da Adobe Sign com [!DNL Veeva Vault] facilita o processo de obtenção de uma assinatura ou aprovação para qualquer documentação que exija assinaturas legais ou processamento de documentos auditáveis.

O processo geral de envio de documentos para assinatura é semelhante ao envio de um email, portanto é fácil de adotar para a maioria dos usuários.

A integração da Adobe Sign com [!DNL Veeva Vault] simplifica e agiliza seus fluxos de trabalho de documentos e assinaturas. Usando o fluxo de trabalho de integração, você:

* Economizando tempo e recursos gastos com correio de caracol, iluminação e fax.
* Envie contratos para assinatura eletrônica ou aprovação de [!DNL Veeva Vault], acesse o histórico de contratos em tempo real e exiba os contratos salvos.
* Monitore as negociações em tempo real em toda a organização e obtenha atualizações quando os contratos são exibidos, assinados, cancelados ou recusados.
* eSign em mais de 20 idiomas e suporte ao serviço de retorno de fax em mais de 50 locais no mundo.
* Crie modelos de contrato reutilizáveis para enviar opções.

## Enviar um contrato usando o Adobe Sign para [!DNL Veeva Vault] {#send-sign-vault-agreement}

Para enviar um contrato usando o Adobe Sign para Veeva:

1. Acesse a [[!DNL Veeva Vault] página de logon](https://login.veevavault.com/) e insira seu nome de usuário e senha. Ele abre a página inicial do seu Cofre, como mostrado abaixo.

   ![](images/vault-home.png)

1. Selecione a guia **[!UICONTROL Biblioteca]** e selecione **[!UICONTROL Criar]** no canto superior direito.

   ![](images/create-library.png)

1. Selecione **[!UICONTROL Carregar e Continuar]**.

1. Faça upload de qualquer documento da unidade local.

1. Na caixa de diálogo exibida, selecione **[!UICONTROL Tipo]** como *[!UICONTROL Clínico]* e selecione um **[!UICONTROL Subtipo]** e **[!UICONTROL Classificação]**, se necessário.

   ![](images/choose-document-type.png)

1. Selecione **[!UICONTROL Ok]** para fechar a caixa de diálogo.

1. Selecione **[!UICONTROL Próximo]**.

1. Na janela exibida, preencha todos os campos obrigatórios na seção de metadados e selecione **[!UICONTROL Salvar]**.

   ![](images/metadata-details.png)

1. Ele cria um documento de teste no status **[!UICONTROL Rascunho]**, conforme exibido abaixo.

   ![](images/document-draft.png)

1. No canto superior direito, selecione o menu suspenso ![ícone de engrenagem](images/icon-gear.png) e selecione **[!UICONTROL Iniciar revisão]**.

   ![](images/start-review.png)

1. Selecione **[!UICONTROL Revisor]** e **[!UICONTROL Data de Vencimento da Revisão]**.

1. Selecione **[!UICONTROL Início]**. Altera o status do documento para [!UICONTROL IN REVIEW].

   ![](images/in-review.png)

1. Conclua a tarefa atribuída em nome dos revisores. Quando terminar, o status do documento será alterado para [!UICONTROL REVIEWED].

   ![](images/reviewed-status.png)

1. Selecione o menu suspenso ![ícone de engrenagem](images/icon-gear.png) e selecione **[!UICONTROL Adobe Sign]**.

   ![](images/select-adobe-sign.png)

1. Na janela do iFrame que é aberta no Vault, insira o endereço de email do destinatário e selecione **[!UICONTROL Próximo]**.

   ![](images/iframe.png)

1. Depois que o documento for processado, arraste e solte os campos de Assinatura no painel direito e selecione **[!UICONTROL Enviar]**.

   ![](images/add-signature-fields.png)

1. Ele envia o documento ao destinatário para assinatura. Depois que o destinatário recebe o email do documento, o status do documento muda de [!UICONTROL Revisado] para [!UICONTROL Na assinatura do Adobe].

   ![](images/in-adobe-signing.png)

1. Depois que todas as assinaturas são capturadas e concluídas no Adobe Sign, o status do documento no Cofre muda para [!UICONTROL Aprovado].

1. Selecione a opção **[!UICONTROL Arquivos de documento]** e expanda a seção **[!UICONTROL Representações]** no Cofre. Ele cria automaticamente uma nova Representação chamada &quot;Representação Adobe Sign&quot; quando o documento está no estado Aprovado.

   ![](images/document-files.png)

1. Baixe a representação da Adobe Sign para validar a assinatura do destinatário.

   ![](images/verify-signature.png)

## Cancelar um contrato usando o Adobe Sign para [!DNL Veeva Vault] {#cancel-sign-vault-agreement}

1. Acesse a [[!DNL Veeva Vault] página de logon](https://login.veevavault.com/) e insira seu nome de usuário e senha. Ele abre a página inicial do seu Cofre, como mostrado abaixo.

   ![](images/vault-home.png)

1. Selecione a guia **[!UICONTROL Biblioteca]** e selecione o documento. O status do documento pode ser: [!UICONTROL No Adobe Sign Draft], [!UICONTROL No Adobe Sign Authoring], ou [!UICONTROL No Adobe Signing].

   ![](images/document-adobe-sign-authoring.png)

1. Selecione **[!UICONTROL Cancelar Adobe Sign]**.

   ![](images/cancel-document.png)

1. Aciona a ação da Web e carrega a janela do iFrame em [!UICONTROL Vault].

   ![](images/cancelled-document.png)

1. O status do documento é alterado automaticamente para [!UICONTROL Revisar].

   ![](images/cancel-reviewed.png)

Depois que o status do documento for alterado para Revisão, você poderá enviá-lo novamente para assinatura.
