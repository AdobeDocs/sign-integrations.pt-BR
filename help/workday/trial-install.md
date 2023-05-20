---
title: Instalação da versão de avaliação do Workday
description: Guia de instalação do Workday para uma conta de avaliação no Adobe Sign
uuid: 0c51f329-b7c1-44a2-88a3-670be7673747
products: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
discoiquuid: 63ed2d5b-9d82-4f87-97e1-2dde23501e89
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: beafe6c0-262f-4f5b-9315-a023a4eef4a2
source-git-commit: 4d73ff36408283805386bd3266b683bc187d6031
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 0%

---

# [!DNL Workday] Instalação de avaliação{#workday-trial-installation}

## Visão geral {#overview}

Este documento foi criado para ajudar [!DNL Workday] os clientes aprendem a ativar uma conta de avaliação no Adobe Sign e depois integrá-la ao [!DNL Workday] locatário. Para usar o Adobe Sign em [!DNL Workday], você deve saber como criar e modificar [!DNL Workday] itens como:

* Estrutura do processo empresarial
* Configuração e configuração do inquilino
* Relatórios e [!DNL Workday] Integração com o Studio

**Observação**: Se você tiver uma conta da Adobe Sign, não há necessidade de iniciar uma versão de avaliação. Você pode entrar em contato com seu Gerente de sucesso do cliente para solicitar [!DNL Workday] integração.

As etapas de alto nível para concluir a integração são:

* Ativar sua conta de avaliação com o Adobe Sign
* Gerar uma chave de integração no Adobe Sign
* Instale a chave de integração no [!DNL Workday] Locatário

## Ativar sua conta de avaliação do Adobe Sign {#activate-sign-trial-account}

Para solicitar uma avaliação de 30 dias do Adobe Sign, você deve preencher este [formulário de registro](https://land.echosign.com/esign-trial-workday-registration.html).

**Observação**: É altamente recomendável usar um endereço de e-mail funcional válido para criar a versão de avaliação, e não um e-mail temporário. Você deve acessar este email para verificar a conta, portanto, o endereço deve ser válido.

![O formulário de solicitação de avaliação](images/trial-land.png)

Em até um dia útil, um especialista de integração da Adobe Sign fornece sua conta (no Adobe Sign) para [!DNL Workday]. Após a conclusão, você receberá um email de confirmação, conforme mostrado abaixo.

![O email de boas-vindas do Adobe Sign](images/welcome-email-2020.png)

Para inicializar sua conta e acessar o Adobe Sign [!UICONTROL Início] siga as instruções no email .

![O painel do Adobe Sign](images/classic-home.png)

## Gerar uma chave de integração {#generate-an-integration-key}

Para novas instalações, você deve gerar uma chave de integração no Adobe Sign e inseri-la em [!DNL Workday]. Essa chave autentica o Adobe Sign e [!DNL Workday] para confiar uns nos outros e compartilhar conteúdo.

Para gerar uma Chave de integração no Adobe Sign:

1. Faça logon no administrador no Adobe Sign.
1. Navegue até **[!UICONTROL **Conta]** > **[!UICONTROL Preferências pessoais]** > **[!UICONTROL Tokens de acesso**]**.
1. Clique no botão **ícone de adição circulado** no lado direito da janela.

   Ela abre o [!UICONTROL Criar Chave de Integração] interface.

   ![Imagem da navegação até a página Tokens de acesso](images/navigate-to-group-accesstokens.png)

1. Forneça um nome intuitivo para a chave, como [!DNL Workday].

   A Chave de integração deve ter os seguintes elementos ativados:

   * agreement_read
   * agreement_write
   * agreement_send
   * widget_read
   * library_read

   ![O painel Criar chave de integração](images/create-integration-key-575.png)

1. Clique em **[!UICONTROL Salvar]**.

   O [!UICONTROL Tokens de acesso] é exibida mostrando as chaves criadas em sua conta.

1. Clique na definição de chave criada para [!DNL Workday].

   O [!UICONTROL Chave de integração] é exposto na parte superior da definição.

1. Clique no botão **[!UICONTROL Chave de integração]** link.

   Ela expõe a chave de integração.

   ![O link da chave de integração](images/integration-key.png)

1. Copie esta chave e salve-a em um local seguro para a próxima etapa.
1. Clique em **[!UICONTROL OK]**.

   ![O painel Chave de integração](images/copy-the-key-575.png)

## Configure o [!DNL Workday] locatário {#configuring-the-workday-tenant}

### Instalar a chave de integração {#install-the-integration-key}

Instalando a Chave de integração no [!DNL Workday] o locatário estabelece a relação de confiança com a Adobe Sign. Quando esse relacionamento estiver estabelecido, qualquer Processo de Negócios poderá ter um [!UICONTROL Etapa Revisão do documento] adicionado que ativa o processo de assinatura.

**Observação**: O Adobe Sign é marcado como &quot;Adobe Document Cloud&quot; em todo o [!DNL Workday] ambiente.

Para instalar a Chave de integração:

1. Fazer logon em [!DNL Workday] como administrador de conta.
1. Procure e abra o **[!UICONTROL Editar configuração de inquilino - Processos corporativos]** página.

1. Forneça informações para os quatro campos a seguir:

   * **[!UICONTROL Reconhecimento Adobe Document Cloud]**: Um reconhecimento de texto fixo da integração.

   * **[!UICONTROL Chave de API do Adobe Document Cloud]**: Onde a Chave de integração está instalada

   * **[!UICONTROL Endereço de Email do Remetente do Adobe Document Cloud]**: O endereço de email do administrador de nível de grupo no Adobe Sign

   * **[!UICONTROL Remover documentos aguardando assinatura eletrônica quando o documento for cancelado]**: Uma configuração opcional que remove documentos do ciclo de assinatura se um documento for cancelado em [!DNL Workday].

   ![Os campos da Chave de integração do Adobe Sign](images/bp-filled-torn2-575.png)

1. Em seguida, conclua a instalação:

   1. Cole a chave de integração na [!UICONTROL Chave de integração de API do Adobe Sign] campo.
   1. Insira o endereço de email do administrador do Adobe Sign no [!UICONTROL Endereço de Email do Remetente do Adobe Document Cloud] campo.
   1. Clique em **[!UICONTROL OK]**.

   ![Os campos Chave de integração e o campo de email do detentor da chave](images/bp-filled-small.png)

A funcionalidade do Adobe Sign agora pode ser adicionada a qualquer Processo corporativo ao adicionar um [!UICONTROL Etapa Revisão do documento] e configurá-lo para uso **[!UICONTROL eSign da Adobe]** como o tipo de assinatura eletrônica.

### Configurar a etapa de revisão de documento {#configure-the-review-document-step}

O documento da etapa de revisão do documento pode ser um documento estático; um documento gerado por uma etapa Gerar Documento dentro do mesmo processo de negócios; ou um relatório formatado criado com o [!DNL Workday] Designer de Relatórios. Todos esses casos podem ser aumentados com [Tags de texto Adobe](https://adobe.com/go/adobesign_text_tag_guide) para controlar a aparência e a posição dos componentes específicos do Adobe Signing. A origem do documento deve ser especificada na definição do processo de negócios. Não é possível carregar um documento ad hoc enquanto o processo de negócios está em execução.

A capacidade de serializar grupos de signatários é exclusiva do uso do Adobe Sign com uma Etapa de revisão de documento. Os grupos de signatários permitem especificar grupos baseados em funções que assinam em sequência. O Adobe Sign não oferece suporte a grupos de assinatura paralelos.

Para obter ajuda para configurar a Etapa Revisão do documento, consulte o [Guia de início rápido](https://adobe.com//go/adobesign_workday_quick_start){target="_blank"}.

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

Os clientes da Adobe Sign devem entrar em contato com o Gerente de sucesso do cliente (CSM) para obter suporte. Como alternativa, o Suporte Técnico da Adobe pode ser contatado por telefone: 1-866-318-4100; aguarde a lista de produtos e digite: 4 e depois 2 (conforme solicitado).

* [Adição de tags de texto Adobe aos documentos](https://adobe.com/go/adobesign_text_tag_guide)

* [Configuração da revisão de documentos e exemplos](https://www.adobe.com//go/adobesign_workday_quick_start){target="_blank"}

[**Entre em contato com o Suporte da Adobe Sign**](https://www.adobe.com/go/adobesign-support-center)
