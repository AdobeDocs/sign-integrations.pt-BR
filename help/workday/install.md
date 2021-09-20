---
title: Guia de instalação do Workday
description: Guia de instalação para habilitar a integração do Adobe Sign com Workday
uuid: 56478222-fe66-4fa5-aac3-0ecdf2863197
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
discoiquuid: 29d55a25-6e2f-4c59-ae7c-c21bb82cecba
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 8f12b524-2123-45d4-98d5-b2b23580a5ea
source-git-commit: ba5e0fccfdb7cd278cc0ae57dc03da1e17b51577
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 26%

---

# [!DNL Workday] Manual de instalação{#workday-installation-guide}

[**Entrar em contato com o Suporte do Adobe Sign**](https://adobe.com/go/adobesign-support-center_br)

## Visão geral {#overview}

Este documento explica como integrar o Adobe Sign ao seu [!DNL Workday] inquilino. Para usar o Adobe Sign em [!DNL Workday], você precisa saber como criar e modificar [!DNL Workday] itens como:

* Estrutura do processo comercial
* Configuração e configuração do inquilino
* Geração de relatórios e [!DNL Workday] integração de estúdio

As etapas de alto nível para concluir a integração são:

* Ativar sua conta administrativa no Adobe Sign (Somente novos clientes)
* Configure um grupo no Adobe Sign para manter o usuário de integração [!DNL Workday]
* Estabelecer a relação OAuth entre [!DNL Workday] e a Adobe Sign

## Ative sua conta da Adobe Sign {#activating-your-adobe-sign-account}

Clientes existentes com contas estabelecidas podem pular para o tópico [Configurar o Adobe Sign para [!DNL Workday]](#config).

Para os clientes que são novos na Adobe Sign e não têm um logon pré-existente, um especialista em integração de Adobe (no Adobe Sign) fornece sua conta para [!DNL Workday]. Após a conclusão, você receberá um email de confirmação, conforme mostrado abaixo.

![Imagem do email de boas-vindas do Adobe Sign](images/welcome-email-2020.png)

Você precisa seguir as instruções no email para inicializar sua conta e acessar a página do Adobe Sign [!UICONTROL Home].

![A página do painel do Adobe Sign](images/classic-home.png)

## Configurar o Adobe Sign para [!DNL Workday] {#config}

Para configurar o Adobe Sign para [!DNL Workday], você precisa gerar os dois objetos dedicados a seguir no sistema Adobe Sign:

* **Um  [!DNL Workday] grupo**:  [!DNL Workday] requer um &quot;grupo&quot; dedicado na conta da Adobe Sign para habilitar a funcionalidade de integração. O grupo Adobe Sign é usado para controlar apenas o uso [!DNL Workday] do Adobe Sign. Qualquer outro uso potencial, como Salesforce.com ou Arriba, não é afetado. As notificações por email são suprimidas no grupo [!DNL Workday] para que os usuários [!DNL Workday] recebam notificações somente na caixa de entrada [!DNL Workday].

* **Um usuário de autenticação para manter a chave** de integração: Um  [!DNL Workday] grupo deve ter apenas um administrador de nível de grupo, que é o detentor autorizado da chave de integração. Recomendamos que o administrador use um endereço de email funcional como `HR@MyDomain.com` em vez de um email pessoal para reduzir o risco de desabilitar o usuário no futuro e, consequentemente, desabilitar a integração.

### Criar um usuário e um grupo no Adobe Sign {#create-a-user-and-group-in-adobe-sign}

Para criar um usuário no Adobe Sign:

1. Faça logon no Adobe Sign como administrador de conta.
1. Navegue até **[!UICONTROL Conta]** > **[!UICONTROL Utilizadores]**.
1. Clique no ícone ![imagem](images/icon_plus.png) para criar um novo usuário.

   ![Imagem do caminho de navegação para criar um novo usuário](images/navigate-to-group-unbranded.png)

1. Na caixa de diálogo que é aberta, forneça os detalhes do novo usuário:

   * Forneça um email funcional que você possa acessar.
   * Insira um valor adequado de Nome e Sobrenome.
   * Selecione **[!UICONTROL Criar um novo grupo para este utilizador]** no Grupo de Utilizadores.
   * Forneça o **[!UICONTROL Nome do novo grupo]** com um nome intuitivo como *[!DNL Workday]*.

   ![O painel Criar um usuário](images/create-user.png)

1. Clique em **[!UICONTROL Salvar]**.

   Ele traz você de volta à página [!UICONTROL Usuários] que lista o novo usuário com um status **[!UICONTROL CRIADO]**.

   ![Uma exibição do novo usuário criado](images/post-user-creation.png)

Para verificar o endereço de email do usuário com o status &quot;Criado&quot;:

1. Faça logon no email do novo usuário.
2. Encontre o email &quot;Bem-vindo à Adobe Sign&quot;.
3. Clique em **[!UICONTROL Clique aqui para definir a senha]**.
4. Definir a senha.

Depois de verificar o endereço de email, o status do usuário muda de [!UICONTROL CRIADO] para [!UICONTROL ATIVO].

![Imagem do novo usuário ativado](images/actived-users-575.png)

### Definir o usuário de autenticação {#define-the-authenticating-user}

Para promover o novo usuário no grupo [!DNL Workday]:

1. Vá até a página [!UICONTROL Usuários] (se já não estiver nela).
2. Clique duas vezes no usuário no grupo [!DNL Workday].

   Isso abre uma página [!UICONTROL Editar] para as permissões do usuário.

3. Verifique **[!UICONTROL Administrador de grupo]**.
4. Clique em **[!UICONTROL Salvar]**.

![](images/user-permissions-edit1-575.png)

## Configurar o inquilino [!DNL Workday] {#configure-workday}

Para concluir a conexão entre o inquilino [!DNL Workday] e o Adobe Sign, precisamos estabelecer uma relação de confiança entre os serviços. Depois de concluído, podemos adicionar uma Etapa de revisão do documento que permite o processo de assinatura por meio do Adobe Sign.

>[!NOTE]
>
>A Adobe Sign tem a marca Adobe Document Cloud em todo o ambiente [!DNL Workday].

Para estabelecer a relação de confiança:

1. Faça logon em [!DNL Workday] como administrador de conta.
1. Abra a página **[!UICONTROL Editar configuração de inquilino - Processos corporativos]**.
1. Localize a seção [!UICONTROL Configuração da assinatura eletrônica]:

   ![](images/esignature_configurations.png)

1. Clique em **[!UICONTROL Autenticar com Adobe]**.

   Isso inicia a sequência de autenticação OAuth2.0.

1. Quando solicitado, forneça as credenciais para o administrador do Adobe Sign Group que você criou anteriormente.
1. Aprovar o acesso ao Adobe Sign.

>[!NOTE]
>
>Certifique-se de fazer logout completo de qualquer outra instância do Adobe Sign antes de continuar.

Depois de conectado, a caixa de seleção Configuração da Adobe ativada é marcada, e você pode começar a usar o Adobe Sign com o [!DNL Workday].

### Configurar a etapa de revisão do documento {#configure-review}

O documento para a Etapa de revisão do documento pode ser um dos seguintes:

* Um documento estático
* Um documento gerado por uma etapa Gerar documento dentro do mesmo processo de negócios
* Um relatório formatado criado com o [!DNL Workday] Designer de Relatórios

Você pode adicionar qualquer um desses documentos com [Tags de texto de Adobe](https://adobe.com/go/adobesign_text_tag_guide_br) para controlar a aparência e a posição dos componentes específicos de Assinatura de Adobe. A fonte do documento deve ser especificada na definição do processo corporativo. Não é possível carregar um documento ad-hoc enquanto o processo corporativo está em execução.

Exclusivo para usar o Adobe Sign com uma Etapa de revisão de documento é a capacidade de ter Grupos de signatários serializados. Isso permite que você especifique grupos com base em funções que assinam em sequência. A Adobe Sign não oferece suporte a grupos de assinatura paralelos.

Para obter assistência na configuração da Etapa de revisão do documento, consulte o [Guia de início rápido](https://adobe.com//go/adobesign_workday_quick_start){target=&quot;_blank&quot;}.

## Suporte {#support}

### [!DNL Workday] apoio {#workday-support}

[!DNL Workday]O é o proprietário da integração e deve ser o seu primeiro ponto de contato em caso de dúvidas sobre o escopo da integração, solicitações de recursos ou problemas nas funções diárias da integração.

Você pode consultar os seguintes artigos da comunidade [!DNL Workday] sobre como solucionar problemas de integração e gerar documentos:

* [Solução de problemas de integrações de eSignature](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [Etapa de revisão de documentos](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)
* [Geração dinâmica de documentos](https://community.workday.com/saml/login?destination=/articles/176443)
* [Ofereça dicas de geração de documentos](https://community.workday.com/node/183242)

### Suporte Adobe Sign {#adobe-sign-support}

O Adobe Sign é o parceiro da integração e deve ser contatado em caso de falha da integração ao obter assinaturas, ou em caso de falha de notificação de assinaturas pendentes.

Os clientes do Adobe Sign devem entrar em contato com o Gerenciador de sucesso do cliente (CSM) para obter suporte. Como alternativa, o Suporte técnico da Adobe pode ser contatado por telefone: 1-866-318-4100. Aguarde a lista de produtos e digite: 4, em seguida, 2 (como solicitado).

* [Adição de tags de texto de Adobe a documentos](https://adobe.com/go/adobesign_text_tag_guide)
* [Revisar a configuração do documento e exemplos](https://www.adobe.com/go/adobesign_workday_quick_start)

## Perguntas comuns {#faq}

### Por que o status não está sendo atualizado em [!DNL Workday] mesmo quando o documento está totalmente assinado? {#why-is-the-status-not-being-updated-within-workday-even-the-document-is-fully-signed}

O status do documento em [!DNL Workday] pode não ser refletido se o candidato não clicar no botão &#39;[!UICONTROL Enviar]&#39; após fazer logon no Adobe Sign.

Conforme a [!DNL Workday] tarefa Verifique o status da assinatura eletrônica: Para iniciar o processo, o usuário pode enviar a tarefa Caixa de entrada associada.

Conforme [!DNL Workday] Desenvolvimento: A assinatura original conclui o processo somente se o usuário enviar a tarefa da caixa de entrada depois de assinar o documento. Após a assinatura, o iframe é fechado e o usuário é redirecionado para a mesma tarefa na qual pode clicar no botão [!UICONTROL Enviar] para concluir o processo.
