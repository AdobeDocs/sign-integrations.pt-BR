---
title: Guia do usuário do Veeva Vault
description: Guia do usuário do Veeva Vault sobre como usar a integração do Adobe Sign com a Veeva
products: Adobe Sign
content-type: reference
locnotes: All languages; screenshots to follow what's there already (seems there is a mix within a given language version of the article)
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 39a43637-af3f-432e-a784-8f472aa86df5
source-git-commit: c164692d78608c436d136caef44b19fe8d37b9d8
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# Adobe Acrobat Sign para [!DNL Veeva Vault]: Guia do usuário {#veeva-vault-user-guide}

[**Entre em contato com o Suporte da Adobe Acrobat Sign**](https://adobe.com/go/adobesign-support-center)

Este documento foi criado para ajudar [!DNL Veeva Vault] os clientes aprendem a usar o Adobe Acrobat Sign para [!DNL Veeva Vault] integração para enviar um contrato.

## Visão geral {#overview}

Integração do Adobe Acrobat Sign com [!DNL Veeva Vault] facilita o processo de obtenção de uma assinatura ou aprovação para qualquer documentação que exija assinaturas legais ou processamento de documentos auditáveis.

O processo geral de envio de documentos para assinatura é semelhante ao de envio de email, por isso é fácil de adotar para a maioria dos usuários.

Integração do Adobe Acrobat Sign com [!DNL Veeva Vault] simplifica e agiliza os fluxos de trabalho de documentos e assinaturas. Usando o fluxo de trabalho de integração, você:

* Poupe tempo e recursos gastos em emails de caracol, envio noturno ou envio de fax.
* Envie contratos para assinatura eletrônica ou aprovação de [!DNL Veeva Vault], acesse o histórico de contratos em tempo real e exiba contratos salvos.
* Acompanhe os negócios em tempo real em toda a organização e receba atualizações quando os contratos forem exibidos, assinados, cancelados ou recusados.
* eSign em mais de 20 idiomas e suporte ao serviço de fax-back em mais de 50 locais no mundo todo.
* Crie Modelos de contrato reutilizáveis para enviar opções.

## Enviar um contrato usando o Adobe Acrobat Sign para [!DNL Veeva Vault] {#send-sign-vault-agreement}

Para enviar um contrato usando o Adobe Acrobat Sign para Veeva:

1. Vá para a [[!DNL Veeva Vault] página de logon](https://login.veevavault.com/) e digite seu nome de usuário e senha. Ela abre a página inicial do Vault, conforme mostrado abaixo.

   ![](images/vault-home.png)

1. Selecionar **[!UICONTROL Biblioteca]** e selecione **[!UICONTROL Criar]** no canto superior direito.

   ![](images/create-library.png)

1. Selecionar **[!UICONTROL Carregar e Continuar]**.

1. Faça upload de qualquer documento na unidade local.

1. Na caixa de diálogo exibida, selecione **[!UICONTROL Tipo]** como *[!UICONTROL Clínico]* e selecione um **[!UICONTROL Subtipo]** e **[!UICONTROL Classificação]**, se necessário.


   ![](images/choose-document-type.png)

1. Para fechar a caixa de diálogo, selecione **[!UICONTROL OK]**.

1. Selecionar **[!UICONTROL Próximo]**.

1. Na janela exibida, preencha todos os campos obrigatórios na seção de metadados e selecione **[!UICONTROL Salvar]**.

   ![](images/metadata-details.png)

1. Ele cria um documento de teste no **[!UICONTROL Rascunho]** como exibido abaixo.

   ![](images/document-draft.png)

1. No canto superior direito, selecione ![ícone de engrenagem](images/icon-gear.png) menu suspenso e selecione **[!UICONTROL Iniciar revisão]**.

   ![](images/start-review.png)

1. Selecione o **[!UICONTROL Revisor]** e **[!UICONTROL Revisar Data de Vencimento]**.

1. Selecionar **[!UICONTROL Iniciar]**. Isso altera o Status do documento para [!UICONTROL EM REVISÃO].

   ![](images/in-review.png)

1. Conclua a tarefa atribuída em nome dos revisores. Depois de concluído, o status do documento é alterado para [!UICONTROL REVISADO].

   ![](images/reviewed-status.png)

1. Selecionar ![ícone de engrenagem](images/icon-gear.png) menu suspenso e selecione **[!UICONTROL Adobe Sign]**.

   ![](images/select-adobe-sign.png)

1. Se o recurso UMG (Usuários em vários grupos) estiver ativado na conta do Adobe Acrobat Sign e o remetente pertencer a vários grupos, você verá uma caixa de diálogo conforme mostrado abaixo. Na caixa de diálogo, selecione o grupo e, em seguida, selecione **[!UICONTROL Próximo]**.

   ![](images/umg-dialog.png)

1. Na janela do iFrame que é aberta no Vault, insira o endereço de email do destinatário e selecione **[!UICONTROL Próximo]**.

   ![](images/iframe.png)

   **Observação:** Se não existir uma conta de usuário do Adobe Acrobat Sign para o email do remetente, a janela do iFrame exibirá uma mensagem, conforme mostrado abaixo. Ele também envia ao usuário um email com as instruções para ativar a conta.

   ![](images/iFrame-registration-message.png)

   ![](images/iFrame-confirm-email.png)

   No entanto, se *Provisionamento automático de usuários do Sign* estiver desativado, a criação do usuário do Adobe Acrobat Sign falha e a janela do iFrame exibe uma mensagem solicitando que o usuário entre em contato com o administrador da conta do Adobe Acrobat Sign. O administrador da conta da Adobe Acrobat Sign pode executar uma das seguintes ações:

   * Ative o *Provisionamento automático de usuários do Sign* para a conta.
   * Crie o usuário no Adobe Acrobat Sign antes de usar a integração do Adobe Acrobat Sign do Veeva Vault.

   ![](images/iFrame-contact-administrator.png)

1. Assim que o documento for processado, arraste e solte os campos de Assinatura no painel direito e selecione **[!UICONTROL Enviar]**.

   ![](images/add-signature-fields.png)

1. Ele envia o documento aos destinatários para assinatura. Depois que o destinatário recebe o email do documento, o status do documento muda de [!UICONTROL Revisado] para [!UICONTROL Assinatura no Adobe].

   ![](images/in-adobe-signing.png)

1. Depois que todas as assinaturas são capturadas e concluídas no Adobe Acrobat Sign, o Status do documento no Vault muda para [!UICONTROL Aprovado].

1. Selecionar **[!UICONTROL Arquivos de documentos]** e expandir a **[!UICONTROL Representações]** no Vault. Ele cria automaticamente uma Representação chamada &quot;Adobe Sign Rendition&quot; quando o documento está no estado Aprovado.

   ![](images/document-files.png)

1. Baixe a Representação do Adobe Sign para validar a assinatura do destinatário.

   ![](images/verify-signature.png)

## Cancelar um contrato usando o Adobe Acrobat Sign para [!DNL Veeva Vault] {#cancel-sign-vault-agreement}

1. Vá para a [[!DNL Veeva Vault] página de logon](https://login.veevavault.com/) e digite seu nome de usuário e senha. Ela abre a página inicial do Vault, conforme mostrado abaixo.

   ![](images/vault-home.png)

1. Selecionar **[!UICONTROL Biblioteca]** e selecione o documento. O status do documento pode ser: [!UICONTROL No Adobe Sign Draft], [!UICONTROL Na criação do Adobe Sign]ou [!UICONTROL Assinatura no Adobe].

   ![](images/document-adobe-sign-authoring.png)

1. Selecionar **[!UICONTROL Cancelar Adobe Sign]**.

   ![](images/cancel-document.png)

1. Aciona a ação da Web e carrega a janela do iFrame no [!UICONTROL Cofre].

   ![](images/cancelled-document.png)

1. O status do documento muda automaticamente para [!UICONTROL Revisar].

   ![](images/cancel-reviewed.png)

Depois que o status do documento mudar para Revisão, você poderá enviá-lo novamente para assinatura.
