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
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 8f12b524-2123-45d4-98d5-b2b23580a5ea
source-git-commit: 4d73ff36408283805386bd3266b683bc187d6031
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 26%

---

# [!DNL Workday] Guia de instalação{#workday-installation-guide}

[**Entrar em contato com o Suporte do Adobe Sign**](https://adobe.com/go/adobesign-support-center_br)

## Visão geral {#overview}

Este documento explica como integrar o Adobe Sign ao seu [!DNL Workday] locatário. Para usar o Adobe Sign em [!DNL Workday], você precisa saber como criar e modificar [!DNL Workday] itens como:

* Estrutura do processo empresarial
* Configuração e configuração do inquilino
* Relatórios e [!DNL Workday] integração do studio

As etapas de alto nível para concluir a integração são:

* Ativar sua conta administrativa no Adobe Sign (somente novos clientes)
* Configure um grupo no Adobe Sign para manter o [!DNL Workday] usuário de integração
* Estabelecer a relação OAuth entre [!DNL Workday] e Adobe Sign

## Ativar sua conta da Adobe Sign {#activating-your-adobe-sign-account}

Os clientes existentes com contas estabelecidas podem pular para a [Configurar o Adobe Sign para [!DNL Workday]](#config) tópico.

Para clientes que ainda não conhecem a Adobe Sign e não têm um logon preexistente, um especialista de integração do Adobe provisiona sua conta (no Adobe Sign) para [!DNL Workday]. Após a conclusão, você receberá um email de confirmação, conforme mostrado abaixo.

![Imagem do email de boas-vindas do Adobe Sign](images/welcome-email-2020.png)

Você precisa seguir as instruções no email para inicializar sua conta e acessar seu Adobe Sign [!UICONTROL Início] página.

![A página do painel do Adobe Sign](images/classic-home.png)

## Configurar o Adobe Sign para [!DNL Workday] {#config}

Para configurar o Adobe Sign para [!DNL Workday], você precisa gerar os seguintes dois objetos dedicados no sistema Adobe Sign:

* **A [!DNL Workday] grupo**: [!DNL Workday] requer um &quot;grupo&quot; dedicado na conta do Adobe Sign para ativar a funcionalidade de integração. O grupo Adobe Sign é usado para controlar apenas o [!DNL Workday] uso do Adobe Sign. Qualquer outro uso potencial, como Salesforce.com ou Arriba, não será afetado. As notificações por email são suprimidas em [!DNL Workday] para que o [!DNL Workday] os usuários recebem notificações apenas dentro de seus [!DNL Workday] caixa de entrada.

* **Um usuário de autenticação para manter a chave de integração**: A [!DNL Workday] o grupo deve ter apenas um administrador de nível de grupo, que é o proprietário autoritativo da chave de integração. Recomendamos que o administrador use um endereço de email funcional, como `HR@MyDomain.com` em vez de um email pessoal para reduzir o risco de ter o usuário desativado no futuro e, consequentemente, desativar a integração.

### Criar um usuário e um grupo no Adobe Sign {#create-a-user-and-group-in-adobe-sign}

Para criar um usuário no Adobe Sign:

1. Faça logon no Adobe Sign como administrador de conta.
1. Navegue até **[!UICONTROL Conta]** > **[!UICONTROL Usuários]**.
1. Clique no botão ![imagem do ícone de adição](images/icon_plus.png) para criar um novo usuário.

   ![Imagem do caminho de navegação para criar um novo usuário](images/navigate-to-group-unbranded.png)

1. Na caixa de diálogo que é aberta, forneça os detalhes do novo usuário:

   * Forneça um email funcional que você possa acessar.
   * Insira um valor adequado de Nome e Sobrenome.
   * Selecionar **[!UICONTROL Criar um novo grupo para este usuário]** do Grupo de usuários.
   * Forneça o **[!UICONTROL Nome do novo grupo]** com um nome intuitivo como *[!DNL Workday]*.

   ![O painel Criar um usuário](images/create-user.png)

1. Clique em **[!UICONTROL Salvar]**.

   Isso o traz de volta ao [!UICONTROL Usuários] que lista o novo usuário com uma **[!UICONTROL CRIADO]** status.

   ![Uma exibição do novo usuário criado](images/post-user-creation.png)

Para verificar o endereço de email do usuário com o status &quot;Criado&quot;:

1. Faça logon no email do novo usuário.
2. Localize o email &quot;Bem-vindo ao Adobe Sign&quot;.
3. Clique em **[!UICONTROL Clique aqui para definir a senha]**.
4. Definir a senha.

Depois de verificar o endereço de email, o status do usuário muda de [!UICONTROL CRIADO] para [!UICONTROL ATIVO].

![Imagem do novo usuário ativado](images/actived-users-575.png)

### Definir o usuário de autenticação {#define-the-authenticating-user}

Para promover o novo usuário no [!DNL Workday] grupo:

1. Vá até a página [!UICONTROL Usuários] (se já não estiver nela).
2. Clique duas vezes no usuário na caixa de diálogo [!DNL Workday] grupo.

   Isso abre um [!UICONTROL Editar] para as permissões de usuário.

3. Verifique o **[!UICONTROL Administrador de grupo]**.
4. Clique em **[!UICONTROL Salvar]**.

![](images/user-permissions-edit1-575.png)

## Configure o [!DNL Workday] locatário {#configure-workday}

Para concluir a conexão entre o [!DNL Workday] locatário e Adobe Sign, precisamos estabelecer uma relação de confiança entre os serviços. Uma vez concluído, podemos adicionar uma etapa de revisão de documento que permite o processo de assinatura por meio do Adobe Sign.

>[!NOTE]
>
>O Adobe Sign é reconhecido como Adobe Document Cloud no [!DNL Workday] ambiente.

Para estabelecer a relação de confiança:

1. Fazer logon em [!DNL Workday] como administrador de conta.
1. Abra o **[!UICONTROL Editar configuração de inquilino - Processos corporativos]** página.
1. Localize a seção [!UICONTROL Configuração da assinatura eletrônica]:

   ![](images/esignature_configurations.png)

1. Clique em **[!UICONTROL Autenticar com Adobe]**.

   Isso inicia a sequência de autenticação OAuth2.0.

1. Quando solicitado, forneça as credenciais para o administrador do Adobe Sign Group que você criou anteriormente.
1. Aprove o acesso ao Adobe Sign.

>[!NOTE]
>
>Certifique-se de fazer logout completo de qualquer outra instância do Adobe Sign antes de continuar.

Depois de conectado, a caixa de seleção Configuração da Adobe ativada é marcada, e você pode começar a usar o Adobe Sign com o [!DNL Workday].

### Configurar a etapa de revisão de documento {#configure-review}

O documento da Etapa de Revisão de documento pode ser um dos seguintes:

* Um documento estático
* Um documento gerado por uma etapa Gerar Documento dentro do mesmo processo de negócios
* Um relatório formatado criado com o [!DNL Workday] Designer de Relatório

Você pode adicionar qualquer um desses documentos com [Tags de texto Adobe](https://adobe.com/go/adobesign_text_tag_guide_br) para controlar a aparência e a posição dos componentes específicos do Adobe Signing. A fonte do documento deve ser especificada na definição do processo corporativo. Não é possível carregar um documento ad-hoc enquanto o processo corporativo está em execução.

A capacidade de serializar grupos de signatários é exclusiva do uso do Adobe Sign com uma Etapa de revisão de documento. Isso permite que você especifique grupos com base em funções que assinam em sequência. O Adobe Sign não oferece suporte a grupos de assinatura paralelos.

Para obter ajuda para configurar a Etapa Revisão do documento, consulte o [Guia de início rápido](https://adobe.com//go/adobesign_workday_quick_start){target=&quot;_blank&quot;}.

## Suporte {#support}

### [!DNL Workday] suporte {#workday-support}

[!DNL Workday]O é o proprietário da integração e deve ser o seu primeiro ponto de contato em caso de dúvidas sobre o escopo da integração, solicitações de recursos ou problemas nas funções diárias da integração.

Consulte o seguinte [!DNL Workday] artigos da comunidade sobre como solucionar problemas de integração e gerar documentos:

* [Solução de problemas de integrações de assinatura eletrônica](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [Etapa Revisão de documentos](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)
* [Geração dinâmica de documentos](https://community.workday.com/saml/login?destination=/articles/176443)
* [Dicas de geração de documentos de oferta](https://community.workday.com/node/183242)

### Suporte ao Adobe Sign {#adobe-sign-support}

O Adobe Sign é o parceiro da integração e deve ser contatado em caso de falha da integração ao obter assinaturas, ou em caso de falha de notificação de assinaturas pendentes.

Os clientes do Adobe Sign devem entrar em contato com o Gerenciador de sucesso do cliente (CSM) para obter suporte. Como alternativa, o Suporte técnico da Adobe pode ser contatado por telefone: 1-866-318-4100. Aguarde a lista de produtos e digite: 4, em seguida, 2 (como solicitado).

* [Adição de tags de texto Adobe a documentos](https://adobe.com/go/adobesign_text_tag_guide)
* [Revisar a configuração do documento e exemplos](https://www.adobe.com//go/adobesign_workday_quick_start)

## Perguntas comuns {#faq}

### Por que o status não está sendo atualizado no [!DNL Workday] mesmo quando o documento estiver totalmente assinado? {#why-is-the-status-not-being-updated-within-workday-even-the-document-is-fully-signed}

O status do documento em [!DNL Workday] pode não refletir se o candidato não clicar em &#39;[!UICONTROL Enviar]&#39; após fazer logon no Adobe Sign.

Conforme [!DNL Workday] tarefa Verificar status de assinatura eletrônica: Para iniciar o processo, o usuário pode enviar a tarefa Caixa de entrada associada.

Conforme [!DNL Workday] Desenvolvimento: A assinatura original concluirá o processo somente se o usuário enviar a tarefa da caixa de entrada após assinar o documento. Após a assinatura, o iframe é fechado e o usuário é redirecionado para a mesma tarefa na qual pode clicar no [!UICONTROL Enviar] para concluir o processo.
