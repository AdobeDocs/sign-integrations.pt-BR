---
title: Guia de instalação do Coupa
description: Guia de instalação para habilitar a integração do Adobe Sign com o Conjunto Coupa BSM
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 12c91be5-afec-4918-a8fc-ceb33bedf98b
source-git-commit: 623307e86f1b32edfbfa59dbd636ff74a6d09b62
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Coupa] Manual de instalação{#coupa-installation-guide}

[**Entrar em contato com o Suporte do Adobe Sign**](https://adobe.com/go/adobesign-support-center_br)

## Visão geral {#overview}

Este documento explica como configurar sua conta da Adobe Sign para integrar [!DNL Coupa BSM Suite] instância para obter assinaturas.

Pré-requisitos:

* Assinatura do Adobe Sign Enterprise, [Adobe Sign Developer Edition](https://www.adobe.com/sign/developer-form.html) ou [Avaliação do Adobe Sign Enterprise](https://www.adobe.com/sign/business.html)
* Acesso de administrador da Adobe Sign
* [!DNL Coupa BSM Suite] Instância padrão ou avançada

As etapas de alto nível para concluir a integração são:

* Configurar um grupo Adobe Sign para uso com [!DNL Coupa BSM Suite]
* Conectar [!DNL Coupa BSM Suite] ao Adobe Sign
* Crie um webhook da Adobe Sign para notificar sua instância [!DNL Coupa BSM Suite]

## Configurar o Adobe Sign Group para [!DNL Coupa BSM Suite] {#configure-adobe-sign-for-coupa}

Para ter um uso dedicado da Adobe Sign para [!DNL Coupa] dentro de uma organização, os administradores devem criar um grupo da Adobe Sign especificamente para uso [!DNL Coupa BSM Suite]. Esse grupo da Adobe Sign deve ter uma única conta de usuário administrador de grupo que atue como conta de serviço. Como essa conta de serviço é usada para todas as solicitações de assinatura, ela deve ser mantida anônima, por exemplo, `Legal@xyz.com`, `Purchasing@xyz.com` ou `CoupaCLM@xyz.com`, em vez de pessoal, como `Bob.Smith@xyz.com`.

### Criar um grupo e um usuário no Adobe Sign {#create-sign-user-group}

Para criar um usuário no Adobe Sign:

1. Faça logon no Adobe Sign como administrador de conta.
1. Navegue até **[!UICONTROL Conta]** > **[!UICONTROL Utilizadores]**.
1. Para criar um novo usuário, clique no ícone ![mais ícone imagem](images/icon_plus.png).
1. Na caixa de diálogo que é aberta, forneça os detalhes do novo usuário:

   1. Forneça um email funcional que você possa acessar.

      * Esse usuário estabelece e mantém o relacionamento OAuth.
      * O endereço de email deve ser um endereço real para verificação.
   1. Insira os valores apropriados para [!UICONTROL Nome] e [!UICONTROL Sobrenome].
   1. No campo [!UICONTROL Grupo Primário], selecione **[!UICONTROL Criar um novo grupo para este utilizador]**.
   1. No campo [!UICONTROL Novo nome de grupo], forneça um nome de grupo intuitivo como *[!DNL Coupa BSM Suite]*.

   ![O painel Criar um usuário](images/create-user.png)

1. Selecione **[!UICONTROL Salvar]**.

   Depois de salvar os detalhes, a página [!UICONTROL Usuários] mostra o novo usuário com um status [!UICONTROL CRIADO].

   ![Uma exibição do novo usuário criado](images/post-user-creation.png)

   O status [!UICONTROL CRIADO] indica que o usuário ainda não verificou seu endereço de email.

1. Para verificar o endereço de email:
   1. Faça logon no email do novo usuário.
   2. Encontre o email &quot;Bem-vindo à Adobe Sign&quot;. Verifique as pastas de spam/lixo eletrônico, se necessário.
   3. Clique em **[!UICONTROL Clique aqui para definir a senha]**
   4. Definir a senha.

   Depois de verificar o endereço de email, o status do usuário muda de [!UICONTROL CRIADO] para [!UICONTROL ATIVO].

   ![Imagem do novo usuário ativado](images/active-user.png)

### Definir o usuário de autenticação {#define-authenticating-user}

Depois de criar um Grupo e um Usuário nesse grupo, você deve tornar o usuário um &quot;Administrador de grupo&quot;.

Para promover o novo usuário no grupo [!DNL Coupa BSM Suite]:

1. Vá até a página [!UICONTROL Usuários] (se já não estiver nela).
2. Clique duas vezes no usuário.

   Ele abre uma página [!UICONTROL Editar] para as permissões do usuário.

3. Na seção Associação de grupo, selecione as opções **[!UICONTROL Administrador de grupo]** e **[!UICONTROL Pode enviar]**.
4. Desmarque as opções **[!UICONTROL O usuário é um administrador de conta]** e **[!UICONTROL O usuário pode assinar documentos]**.
5. Clique em **[!UICONTROL Salvar]**.

   ![Imagem das configurações do usuário](images/user-settings.png)

## Configurar a instância [!DNL Coupa BSM Suite] {#configure-coupa}

Para concluir a conexão entre a instância [!DNL Coupa BSM Suite ] e a Adobe Sign, deve ser estabelecida uma relação de confiança entre os serviços.

Para configurar o [!DNL Coupa BSM Suite]:

1. Conecte sua instância [!DNL Coupa BSM Suite] à sua conta de serviço da Adobe Sign que você criou acima.
1. Crie uma instância do Adobe Sign Webhook para notificar sua instância do Coupa BSM Suite sobre atualizações em contratos.

Para obter mais detalhes sobre como conectar o [!DNL Coupa BSM Suite] e como criar e registrar o webhook, consulte [Documentação de suporte da instância do Adobe Sign Coupa BSM Suite](https://success.coupa.com/Support/Docs/Power_Apps/CLM_Standard/Signing_and_Approvals/Enable_E-Signatures_Through_Adobe_Sign_and_DocuSign){target=&quot;_blank&quot;}.

## Criar [!DNL Webhook] no Adobe Sign {#create-webhook}

A integração do Coupa CLM usa as notificações do webhook da Adobe Sign para enviar atualizações sobre o estado do contrato. É crítico concluir a configuração do webhook, caso contrário, os contratos enviados para assinatura permanecerão incompletos ou os contratos assinados não serão entregues de volta ao Coupa CLM.

Para criar webhook no Adobe Sign:

1. Faça logon no Adobe Sign usando o usuário administrador de grupo criado acima, por exemplo `coupaclm@MyDomain.com`.

1. Navegue até **Grupos** > **Webhooks**.

   ![Imagem das configurações do usuário](images/webhook-login.png)

1. Para criar uma nova conexão, selecione o ícone ![mais ícone imagem](images/icon_plus.png).

1. Na caixa de diálogo Criar que é aberta, preencha os campos obrigatórios.

   **Observação:** é necessário obter o URL do manipulador de webhook do Coupa.

   ![Imagem das configurações do usuário](images/webhook-create.png)

1. Selecione os parâmetros de notificação necessários.

1. Selecione **Salvar**.

## Suporte {#support}

### [!DNL Coupa BSM Suite] apoio {#coupa-support}

[!DNL Coupa BSM Suite ] é o proprietário da integração e deve ser seu primeiro ponto de contato para perguntas sobre o escopo da integração, solicitações de recursos ou problemas na função diária da integração.

Para qualquer consulta, entre em contato com o [Suporte do Coupa](https://success.coupa.com/Support/Welcome_to_Coupa_Support){target=&quot;_blank&quot;}.

### Suporte Adobe Sign {#adobe-sign-support}

A Adobe Sign é o parceiro de integração e deve ser contatada se a integração não conseguir obter assinaturas ou se a notificação de assinaturas pendentes falhar.

Para obter ajuda com o uso ou configuração da Adobe Sign, você pode entrar em contato com o Gerente de Sucesso do Cliente (CSM) ou entre em contato com o [Suporte da Adobe Sign](https://adobe.com/go/adobesign-support-center).

Os administradores da Adobe Sign também podem abrir tickets e obter suporte por meio da Ajuda (?) no canto superior direito do portal da Adobe Sign.

![Imagem da ajuda do portal da Adobe Sign](images/sign-portal-help.png)
