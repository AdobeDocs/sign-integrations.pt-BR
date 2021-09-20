---
title: A instalação da avaliação do Workday
description: Guia de instalação do Workday para uma conta de avaliação no Adobe Sign
uuid: 0c51f329-b7c1-44a2-88a3-670be7673747
products: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
discoiquuid: 63ed2d5b-9d82-4f87-97e1-2dde23501e89
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: beafe6c0-262f-4f5b-9315-a023a4eef4a2
source-git-commit: 78d6cafa720b41bd638c2ef723b2d4a2def19cd5
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 40%

---

# [!DNL Workday] Instalação da versão de avaliação{#workday-trial-installation}

## Visão geral {#overview}

Este documento foi desenvolvido para ajudar [!DNL Workday] os clientes a aprenderem como ativar uma conta de avaliação com a Adobe Sign e depois integrá-la ao inquilino [!DNL Workday]. Para usar o Adobe Sign em [!DNL Workday], você precisa saber como criar e modificar [!DNL Workday] itens como:

* Estrutura do processo comercial
* Configuração e configuração do inquilino
* Integração com o Reporting and [!DNL Workday] Studio

**Nota**: Se você tiver uma conta Adobe Sign existente, não será necessário iniciar uma avaliação. Você pode entrar em contato com o Gerente de sucesso do cliente para solicitar a integração [!DNL Workday].

As etapas de alto nível para concluir a integração são:

* Ativar a conta de avaliação com o Adobe Sign
* Gerar uma chave de integração no Adobe Sign
* Instale a chave de integração no inquilino [!DNL Workday]

## Ative sua conta de avaliação da Adobe Sign {#activate-sign-trial-account}

Para solicitar uma avaliação de 30 dias da Adobe Sign, você precisa preencher este [formulário de registro](https://land.echosign.com/esign-trial-workday-registration.html).

**Nota**: Recomendamos que você use um endereço de email funcional válido para criar a versão de avaliação e não um email temporário. Você precisa acessar este email para verificar a conta, portanto o endereço deve ser válido.

![O formulário de solicitação de avaliação](images/trial-land.png)

Dentro de um dia útil, um especialista de integração da Adobe Sign fornece sua conta (no Adobe Sign) para [!DNL Workday]. Após a conclusão, você receberá um email de confirmação, conforme mostrado abaixo.

![O email de Boas-vindas do Adobe Sign](images/welcome-email-2020.png)

Siga as instruções no email para inicializar sua conta e acessar a página do Adobe Sign [!UICONTROL Home].

![O painel da Adobe Sign](images/classic-home.png)

## Gerar uma chave de integração {#generate-an-integration-key}

Para novas instalações, você precisa gerar uma chave de integração no Adobe Sign e inseri-la em [!DNL Workday]. Essa chave autentica os ambientes Adobe Sign e [!DNL Workday] para confiar um no outro e compartilhar conteúdo.

Para gerar uma Chave de integração no Adobe Sign:

1. Faça logon como administrador no Adobe Sign.
1. Navegue até **[!UICONTROL **Conta]** > **[!UICONTROL Preferências pessoais]** > **[!UICONTROL Tokens de acesso**]**.
1. Clique no ícone de **círculo com sinal positivo** no lado direito da janela.

   Ele abre a interface [!UICONTROL Criar chave de integração].

   ![Imagem da navegação até a página de Tokens de acesso](images/navigate-to-group-accesstokens.png)

1. Forneça um nome intuitivo para sua chave, como [!DNL Workday].

   A Chave de integração deve ter os seguintes elementos habilitados:

   * agreement_read
   * agreement_write
   * agreement_send
   * widget_read
   * library_read

   ![O painel Criar chave de integração](images/create-integration-key-575.png)

1. Clique em **[!UICONTROL Salvar]**.

   A página [!UICONTROL Tokens de acesso] é exibida, mostrando as chaves criadas para sua conta.

1. Clique na definição da chave criada para [!DNL Workday].

   O link da [!UICONTROL Chave de integração] está exposto na parte superior da definição.

1. Clique no link da **[!UICONTROL Chave de integração.]**

   Ele expõe a chave de integração.

   ![O link da Chave de integração](images/integration-key.png)

1. Copie a chave e salve-a em um local seguro para a próxima etapa.
1. Clique em **[!UICONTROL OK]**.

   ![O painel da Chave de integração](images/copy-the-key-575.png)

## Configurar o inquilino [!DNL Workday] {#configuring-the-workday-tenant}

### Instale a chave de integração {#install-the-integration-key}

Instalar a Chave de integração no inquilino [!DNL Workday] estabelece a relação de confiança com a Adobe Sign. Quando esse relacionamento estiver em vigor, qualquer Processo corporativo poderá ter uma [!UICONTROL Etapa de revisão do documento] adicionada que habilite o processo de assinatura.

**Observação**[!DNL Workday]: o Adobe Sign é reconhecido como “Adobe Document Cloud” no ambiente do 

Para instalar a Chave de integração:

1. Faça logon em [!DNL Workday] como administrador de conta.
1. Procure e abra a página **[!UICONTROL Editar configuração de inquilino - Processos corporativos]**.

1. Forneça informações para os quatro seguintes campos:

   * **[!UICONTROL Reconhecimento]** Adobe Document Cloud: Um reconhecimento de texto fixo da integração.

   * **[!UICONTROL Chave]** da API Adobe Document Cloud: Onde a Chave de integração está instalada

   * **[!UICONTROL Endereço]** de email do remetente da Adobe Document Cloud: O endereço de email do administrador de nível de grupo no Adobe Sign

   * **[!UICONTROL Remova documentos aguardando eSignature quando o documento for cancelado]**: Uma configuração opcional que remove documentos do ciclo de assinatura se um documento for cancelado em  [!DNL Workday].

   ![Os campos da Chave de integração do Adobe Sign](images/bp-filled-torn2-575.png)

1. Em seguida, conclua a instalação:

   1. Cole a Chave de integração no campo [!UICONTROL Chave de integração da API do Adobe Sign.]
   1. Insira o endereço de email do administrador do Adobe Sign no campo [!UICONTROL Endereço de email do remetente da Adobe Document Cloud.]
   1. Clique em **[!UICONTROL OK]**.

   ![Campos da Chave de integração e campo de email do detentor da chave](images/bp-filled-small.png)

A funcionalidade Adobe Sign agora pode ser adicionada a qualquer Processo corporativo adicionando uma [!UICONTROL Etapa de revisão do documento] e configurando-a para usar **[!UICONTROL eSign por Adobe]** como o tipo de eSignature.

### Configurar a etapa de revisão do documento {#configure-the-review-document-step}

O documento da Etapa de revisão do documento pode ser um documento estático; um documento gerado por uma etapa Gerar documento dentro do mesmo processo comercial; ou, um relatório formatado criado com o [!DNL Workday] Designer de relatórios. Todos esses casos podem ser aumentados com [Tags de texto da Adobe](https://adobe.com/go/adobesign_text_tag_guide_br) para controlar o visual e a posição de componentes específicos do Adobe Sign. A fonte do documento deve ser especificada na definição do processo corporativo. Não é possível fazer upload de um documento ad hoc enquanto o processo de negócios estiver em execução.

Exclusivo para usar o Adobe Sign com uma Etapa de revisão de documento é a capacidade de ter Grupos de signatários serializados. Os grupos de signatários permitem especificar grupos com base em funções que assinam em sequência. A Adobe Sign não oferece suporte a grupos de assinatura paralelos.

Para obter assistência na configuração da Etapa de revisão do documento, consulte o [Guia de início rápido](https://adobe.com//go/adobesign_workday_quick_start){target=&quot;_blank&quot;}.

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

Os clientes do Adobe Sign devem entrar em contato com o Gerenciador de sucesso do cliente (CSM) para obter suporte. Como alternativa, o Suporte Técnico de Adobe pode ser acessado por telefone: 1-866-318-4100; aguarde a lista de produtos e insira: 4 e 2 (conforme solicitado).

* [Adicionar tags de texto da Adobe aos documentos](https://adobe.com/go/adobesign_text_tag_guide)

* [Configuração da revisão de documentos e exemplos](https://www.adobe.com//go/adobesign_workday_quick_start)

[**Entrar em contato com o Suporte do Adobe Sign**](https://adobe.com/go/adobesign-support-center_br)
