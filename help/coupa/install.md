---
title: Guia de instalação do Coupa
description: Guia de instalação para habilitar a integração do Adobe Sign com o Coupa BSM Suite
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 12c91be5-afec-4918-a8fc-ceb33bedf98b
source-git-commit: 4d73ff36408283805386bd3266b683bc187d6031
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 7%

---

# [!DNL Coupa] Guia de instalação{#coupa-installation-guide}

[**Entrar em contato com o Suporte do Adobe Sign**](https://adobe.com/go/adobesign-support-center_br)

## Visão geral {#overview}

Este documento explica como configurar sua conta da Adobe Sign para integrar [!DNL Coupa BSM Suite] para obter assinaturas.

Pré-requisitos:

* Assinatura do Adobe Sign Enterprise, [Adobe Sign Developer Edition](https://www.adobe.com/sign/developer-form.html)ou [Avaliação do Adobe Sign Enterprise](https://www.adobe.com/sign/business.html)
* Acesso de administrador do Adobe Sign
* [!DNL Coupa BSM Suite] Instância Padrão ou Avançada

As etapas de alto nível para concluir a integração são:

* Configurar um Adobe Sign Group para uso com [!DNL Coupa BSM Suite]
* Conectar [!DNL Coupa BSM Suite] para o Adobe Sign
* Crie um webhook do Adobe Sign para notificar [!DNL Coupa BSM Suite] instância

## Configurar o Adobe Sign Group para [!DNL Coupa BSM Suite] {#configure-adobe-sign-for-coupa}

Para ter um uso dedicado do Adobe Sign para [!DNL Coupa] em uma organização, os administradores devem criar um grupo da Adobe Sign especificamente para [!DNL Coupa BSM Suite] uso. Esse grupo do Adobe Sign deve ter uma única conta de usuário administrador de grupo que atue como a conta de serviço. Como essa conta de serviço é usada para todas as solicitações de assinatura, ela deve ser mantida anônima, por exemplo, `Legal@xyz.com`, `Purchasing@xyz.com`ou `CoupaCLM@xyz.com`, em vez de pessoal, como `Bob.Smith@xyz.com`.

### Criar um grupo e um usuário no Adobe Sign {#create-sign-user-group}

Para criar um usuário no Adobe Sign:

1. Faça logon no Adobe Sign como administrador de conta.
1. Navegue até **[!UICONTROL Conta]** > **[!UICONTROL Usuários]**.
1. Para criar um novo usuário, clique no botão ![imagem do ícone de adição](images/icon_plus.png) ícone.
1. Na caixa de diálogo que é aberta, forneça os detalhes do novo usuário:

   1. Forneça um email funcional que você possa acessar.

      * Este usuário estabelece e mantém a relação OAuth.
      * O endereço de email deve ser um endereço real para verificação.
   1. Insira os valores apropriados para [!UICONTROL Nome] e [!UICONTROL Sobrenome].
   1. No menu [!UICONTROL Grupo principal] , selecione **[!UICONTROL Criar um novo grupo para este usuário]**.
   1. No menu [!UICONTROL Nome do Novo Grupo] forneça um nome de grupo intuitivo como *[!DNL Coupa BSM Suite]*.

   ![O painel Criar um usuário](images/create-user.png)

1. Selecionar **[!UICONTROL Salvar]**.

   Depois de salvar os detalhes, o [!UICONTROL Usuários] mostra o novo usuário com uma [!UICONTROL CRIADO] status.

   ![Uma exibição do novo usuário criado](images/post-user-creation.png)

   O [!UICONTROL CRIADO] indica que o usuário ainda não verificou o endereço de email.

1. Para verificar o endereço de email:
   1. Faça logon no email do novo usuário.
   2. Localize o email &quot;Bem-vindo ao Adobe Sign&quot;. Verifique as pastas de spam/lixo eletrônico, se necessário.
   3. Clique em **[!UICONTROL Clique aqui para definir a senha]**
   4. Definir a senha.

   Depois de verificar o endereço de email, o status do usuário muda de [!UICONTROL CRIADO] para [!UICONTROL ATIVO].

   ![Imagem do novo usuário ativado](images/active-user.png)

### Definir o usuário de autenticação {#define-authenticating-user}

Depois de criar um Grupo e um Usuário nesse grupo, você deve tornar o usuário um &quot;Administrador do grupo&quot;.

Para promover o novo usuário no [!DNL Coupa BSM Suite] grupo:

1. Vá até a página [!UICONTROL Usuários] (se já não estiver nela).
2. Clique duas vezes no usuário.

   Ela abre um [!UICONTROL Editar] para as permissões de usuário.

3. Na seção Associação de grupo , selecione o **[!UICONTROL Administrador de grupo]** e **[!UICONTROL Pode enviar]** opções.
4. Desmarque a **[!UICONTROL O usuário é um administrador de conta]** e **[!UICONTROL O usuário pode assinar documentos]** opções.
5. Clique em **[!UICONTROL Salvar]**.

   ![Imagem das configurações do usuário](images/user-settings.png)

## Configure o [!DNL Coupa BSM Suite] instância {#configure-coupa}

Para concluir a conexão entre o [!DNL Coupa BSM Suite ] e a Adobe Sign, deve ser estabelecida uma relação de confiança entre os serviços.

Para configurar o [!DNL Coupa BSM Suite]:

1. Conecte seu [!DNL Coupa BSM Suite] instância para sua conta de serviço da Adobe Sign criada acima.
1. Crie uma instância de webhook do Adobe Sign para notificar sua instância do Coupa BSM Suite sobre atualizações de contratos.

Para obter mais detalhes sobre como conectar o [!DNL Coupa BSM Suite] e como criar e registrar o webhook, consulte [Documentação de suporte da instância do Adobe Sign Coupa BSM Suite](https://success.coupa.com/Support/Docs/Power_Apps/CLM_Standard/Signing_and_Approvals/Enable_E-Signatures_Through_Adobe_Sign_and_DocuSign){target=&quot;_blank&quot;}.

## Criar [!DNL Webhook] no Adobe Sign {#create-webhook}

A integração do Coupa CLM usa notificações de webhook do Adobe Sign para enviar atualizações sobre o estado do contrato. É essencial concluir a configuração do webhook, caso contrário, os contratos enviados para assinatura permanecerão incompletos ou os contratos assinados não serão entregues novamente no Coupa CLM.

Para criar um webhook no Adobe Sign:

1. Faça logon no Adobe Sign usando o usuário administrador de grupo criado acima, por exemplo `coupaclm@MyDomain.com`.

1. Navegue até **Grupos** > **Webhooks**.

   ![Imagem das configurações do usuário](images/webhook-login.png)

1. Para criar uma nova conexão, selecione o ![imagem do ícone de adição](images/icon_plus.png) ícone.

1. Na caixa de diálogo Criar que é aberta, preencha os campos necessários.

   **Observação:** Você precisa obter o URL para o manipulador de webhook de Coupa.

   ![Imagem das configurações do usuário](images/webhook-create.png)

1. Selecione os parâmetros de notificação necessários.

1. Selecionar **Salvar**.

## Suporte {#support}

### [!DNL Coupa BSM Suite] suporte {#coupa-support}

[!DNL Coupa BSM Suite ] é o proprietário da integração e deve ser seu primeiro ponto de contato para perguntas sobre o escopo da integração, solicitações de recursos ou problemas na função diária da integração.

Para quaisquer consultas, entre em contato com [Suporte ao Coupa](https://success.coupa.com/Support/Welcome_to_Coupa_Support){target=&quot;_blank&quot;}.

### Suporte ao Adobe Sign {#adobe-sign-support}

O Adobe Sign é o parceiro de integração e deve ser contatado se a integração não conseguir obter assinaturas ou se a notificação de assinaturas pendentes falhar.

Para obter ajuda para usar ou configurar o Adobe Sign, entre em contato com seu Gerente de sucesso do cliente (CSM) ou entre em contato com [Suporte ao Adobe Sign](https://adobe.com/go/adobesign-support-center).

Os administradores do Adobe Sign também podem abrir tickets e obter suporte através da Ajuda (?) no canto superior direito do portal do Adobe Sign.

![Imagem da ajuda do portal do Adobe Sign](images/sign-portal-help.png)
