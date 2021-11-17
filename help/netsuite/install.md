---
title: Adobe Sign para [!DNL NetSuite] - Guia de instalação e personalização (v4.0.4)
description: Adobe Sign para [!DNL NetSuite] - Guia de instalação e personalização
product: Adobe Sign
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 378cac01-87c9-4288-8839-482121d49402
source-git-commit: 7ded835b48519cba656f160e691c697c91e2c8d0
workflow-type: tm+mt
source-wordcount: '4870'
ht-degree: 1%

---

# [!DNL NetSuite] Guia de instalação e personalização (v4.0.4) {#install-customize-NetSuite}

## Visão geral {#overview}

Adobe Sign para [!DNL NetSuite] fornece uma integração completa de eSignature com [!DNL NetSuite]. Você pode usar o Adobe Sign para [!DNL NetSuite] integração para enviar contratos, como contratos, cotas e outros documentos, que exigem assinaturas eletrônicas, diretamente aos destinatários [!DNL NetSuite]. Você pode criar e enviar contratos da Adobe Sign de clientes, lead, cota e outros [!DNL NetSuite] registros. Atualizações da Adobe Sign [!DNL NetSuite] com o status de contratos e armazena os contratos com o [!DNL NetSuite] após serem totalmente executados. Você pode exibir o histórico de todos os contratos enviados de [!DNL NetSuite] de dentro do produto.

Consulte o [Adobe Sign para [!DNL NetSuite] notas de versão](https://experienceleague.adobe.com/docs/sign-integrations/using/netsuite/release-notes.html?lang=en) para obter mais informações.

## Instalar o pacote e configurar o OAuth {#install}

Somente um [!DNL NetSuite] o administrador pode instalar ou atualizar o pacote. Para configurar o OAuth, [!DNL NetSuite] o administrador deve ter acesso de administrador ao Adobe Sign. Antes de instalar o pacote na sua conta de Produção, você deve instalar e testar o pacote em uma [!DNL NetSuite] Conta do Sandbox.

Consulte [Criar um contrato da Adobe Sign](#createagreement) para obter mais informações sobre testes.

>[!CAUTION]
>
>Os clientes que atualizam para a v4.0.4 NÃO devem remover a chave de API existente.
>
>Consulte [Definir preferências personalizadas](#configure) para obter mais informações sobre como a chave da API é usada.

### Instale o pacote pela primeira vez

1. Navegue até [!UICONTROL **Personalização > SuiteBundler > Pesquisar e instalar pacotes**].

1. No *Pesquisar e instalar pacotes* página, insira **Adobe Sign** como palavra-chave e selecione **[!UICONTROL Pesquisar]**.

1. Selecione o **Adobe Sign** nome do pacote.

   ![Procurar o pacote](images/search-for-the-bundle.png)

1. No *[!UICONTROL Detalhes do pacote]* página, selecione **[!UICONTROL Instalar]**.
1. Na *[!UICONTROL Instalação do pacote de visualização]* página, selecione **[!UICONTROL Instalar pacote]**.

   (Não é necessário alterar nenhum dos valores padrão na página)

   ![Instalar o pacote](images/bundle-details-install.png)

1. Na caixa de diálogo Instalar exibida, selecione **[!UICONTROL OK]** para continuar.

   Durante o processo de instalação, o status do pacote é exibido como *[!UICONTROL Pendente]*.

   ![Instalação de pacotes](images/installing-bundles.png)

1. Para exibir um status atualizado, selecione **[!UICONTROL Atualizar]**.

   Após o término da instalação do pacote, *Adobe Sign para[!DNL NetSuite]* no *[!UICONTROL Pacotes instalados]* página.

   ![Pacotes instalados](images/installed-bundles.png)

1. Se você já é uma conta de cliente da Adobe Sign, siga as etapas para  [Configurar o OAuth após a instalação ou atualização](#oauth).

   Se você não tiver uma conta da Adobe Sign, poderá [cadastre-se para uma avaliação corporativa](https://esign.adobe.com/adobe-sign-)[!DNL NetSuite]-test-registration.html) para testar o sistema. Siga as etapas de registro online para ativar sua conta da Adobe Sign.

## Configurar o OAuth após a instalação ou atualização {#oauth}

A Adobe Sign usa o OAuth 2.0 para autenticar sua conta da Adobe Sign no [!DNL NetSuite].

Este protocolo autoriza a instalação [!DNL NetSuite] pacote para se comunicar com a Adobe Sign sem solicitar sua senha. Já que informações confidenciais não está sendo compartilhadas diretamente entre os aplicativos, sua conta tem menos probabilidade de ficar comprometida.

Essa autenticação não afeta sua implementação, mas você deve fazer uma configuração única após instalar ou atualizar o pacote em sua conta de Produção ou Sandbox.

O [!DNL NetSuite] administrador que configura o OAuth também deve ter um acesso de administrador no nível da conta ao Adobe Sign.

1. Em [!DNL NetSuite], navegue até o *Adobe Sign Config* página da lista.

1. Procurar **[!UICONTROL Adobe Sign Config]** (um tipo de registro personalizado) usando o campo Pesquisar no cabeçalho.

1. Na página Resultados da pesquisa, selecione **Exibir** para *Adobe Sign Config* gravar.

   ![Procure por Adobe Sign](images/search-for-adobesignconfig.png)

1. Na página Lista de configurações da Adobe Sign, selecione **[!UICONTROL Exibir]** para *Uso do OAuth para acessar APIs da Adobe Sign* gravar.

   ![Lista de configurações da Adobe Sign](images/adobe-sign-configlist.png)

1. Na página Adobe Sign Config, selecione **[!UICONTROL Faça Logon Com O Adobe Sign]**

   ![Faça logon ](images/log-in-with-adobesign.png)

1. Na página de logon do Adobe Sign exibida, insira suas credenciais e selecione **[!UICONTROL Fazer logon]**.

   ![autenticar no Adobe Sign](images/8-authenticate-toadobesign-2020.png)

1. Na página Confirmar acesso (para OAuth) exibida, selecione **[!UICONTROL Permitir acesso]**

   ![Permitir acesso](images/confirm-access.png)

1. Quando a autorização estiver concluída, você será redirecionado de volta à página Adobe Sign Config em [!DNL NetSuite], conforme mostrado abaixo.

   ![OAuth bem-sucedido](images/successful-oauth.png)

   >[!NOTE]
   >
   >Ao configurar o OAuth na conta do Sandbox, você pode encontrar o erro &quot;Não foi possível determinar a ID da composição do cliente&quot; quando a autorização é concluída.
   >
   >
   >Para continuar, você deve alterar a parte do domínio da conta do URL (sistema).[!DNL NetSuite].com) no seu navegador para apontar para o [!DNL NetSuite] Sandbox da seguinte forma:
   >
   >
   >Alterar:
   >
   >
   >sistema.[!DNL NetSuite].com/app/site/hosting/scriptlet.nl?script=745&amp;deployment=1&amp;web_access_point=https://echosign.com
   >
   >
   >Para:
   >
   >
   >sistema.**sandbox.**[!DNL NetSuite].com/app/site/hosting/scriptlet.nl?script=745&amp;deployment=1&amp;web_access_point=https://echosign.com

## Atualizar o pacote (usuários existentes)

[!DNL NetSuite] atualizações de pacote são lançadas regularmente pelo Adobe. Usuários existentes da Adobe Sign para [!DNL NetSuite] a integração pode atualizar para o pacote mais recente.

>[!CAUTION]
>
>Os clientes que atualizam para uma versão mais recente NÃO devem remover a chave de API existente.
>
>Consulte [Definir preferências personalizadas](#configure) para obter mais informações sobre como a chave da API é usada.

### Pré-requisitos {#prerequisites}

O tempo necessário para atualizar para o pacote v4.0.4 depende do número de contratos que têm o status &quot;Enviado para assinatura&quot;. Geralmente, leva de 7 a 10 minutos para atualizar 100 contratos. Anote o número de registros para estimar a hora da atualização.

Para determinar o número de contratos enviados para assinatura:

1. Navegue até **[!UICONTROL Personalização > Listas, Registros e Arquivos > Tipos de registro]** e, em seguida, localize *Contrato da Adobe Sign.*

   Ou procure Contratos da Adobe Sign na barra de pesquisa.

1. Para [!UICONTROL Contratos da Adobe Sign] gravar, selecionar **[!UICONTROL Pesquisar]**.

   ![Pesquisar Tipos de Registro](images/search-adobe-signagreements.png)

1. Na **[!UICONTROL Status]** menu suspenso, selecione **[!UICONTROL Enviado para assinatura]** e selecione **[!UICONTROL Enviar]**.

   ![Enviar para assinatura](images/submit-search-foragreements.png)

   Anote o número de registros para estimar a hora da atualização.

   ![Anote o número](images/search-results.png)

### Atualizar o pacote {#updating-the-bundle}

1. Navegue até **[!UICONTROL Personalização > SuiteBundler > Pesquisar e instalar > Lista]** e localize seu pacote atual, conforme mostrado abaixo.

   >[!NOTE]
   >
   >Se houver uma nova versão do pacote, um ícone de ponto de exclamação será exibido à direita do *Versão* número do seu pacote atual.

1. No menu suspenso Ação, selecione **[!UICONTROL Atualização]**.

   ![Atualizar ação](images/update-action.png)

1. Na página Visualizar atualização do pacote, selecione **[!UICONTROL Atualizar pacote]** sem alterar qualquer um dos valores padrão exibidos na página.

   Durante a instalação, o status do pacote é exibido como *Pendente*.

   ![Visualizar atualização do pacote](images/preveiw-bundles-update.png).

   >[!NOTE]
   >
   >Ao atualizar o pacote, você pode receber uma mensagem de aviso conforme mostrado abaixo. Se você não personalizou seu [!DNL NetSuite] Registros de assinatura eletrônica, você pode continuar. Se não tiver certeza, é sugerido que você instale o pacote em uma conta Sandbox para testá-lo primeiro antes de atualizar o pacote em uma conta de produção.

   ![Mensagem de erro](images/netsuite-error.png)

1. Para exibir um status atualizado, selecione **[!UICONTROL Atualizar]**.

   ![Instalação da atualização](images/installing-upgrade.png)

   >[!NOTE]
   >
   >Se a atualização estiver demorando devido a vários contratos com um *Enviado para assinatura* , você pode verificar **[!UICONTROL Log de execução]** subguia para o *Instalação do pacote Adobe Sign* para determinar o progresso da atualização. Consulte [Determinando o progresso da atualização](#determineprogress) para obter mais informações.

   Após a conclusão da atualização do pacote, *Adobe Sign para[!DNL NetSuite]* no *Pacotes instalados* página.

   ![Pacote instalado](images/4-installed-bundles.png)

## Configurar o pacote {#configure}

### Definir preferências personalizadas  {#set-custom-preferences}

Você pode usar preferências personalizadas para especificar como os contratos são criados e armazenados em [!DNL NetSuite]. Além disso, o *Provisionamento automático do usuário no Adobe Sign* permite especificar se [!DNL NetSuite] os usuários são provisionados automaticamente nos serviços do Sign quando enviam contratos de [!DNL NetSuite].

1. Navegue até **[!UICONTROL Configuração > Empresa > Preferências gerais]**.
1. Role a página para baixo e selecione o **[!UICONTROL Preferências personalizadas]** subguia.

   ![Preferências personalizadas](images/custom-preferences.png)

1. Ative e configure suas preferências do Adobe Sign conforme necessário:

   * **Digite a chave da API do EchoSign para sua conta**: Não adicione ou edite nenhum valor neste campo.
   * **Usar Contato de Registro Pai como Signatário**: Se ativado, o contato do registro pai é assumido como o primeiro signatário quando os contratos são criados. O remetente pode remover ou editar facilmente o signatário padrão ou adicionar outros signatários ao contrato antes de enviá-lo.
   * **Usar Trans. Contato como signatário, se presente**: Essa preferência só é válida se *Usar Contato de Registro Pai como Signatário* a preferência também está ativada. Se ativado, ao gerar um contrato a partir de um Registro de Transação (por exemplo, Cota), o contato principal da Transação assume o padrão como o primeiro signatário. Consulte [Registros de transação](#transrecords) para obter mais informações. Se não houver contato principal de transação ou se estiver enviando de [!DNL NetSuite] registro do objeto (por exemplo, registro do cliente, registro do parceiro), o destinatário padrão é o contato principal para o email do cliente. O remetente pode remover ou editar facilmente o signatário padrão ou adicionar outros signatários ao contrato antes de enviá-lo.
   * **Permitir a marcação de destinatários como aprovadores**: Se ativado, os remetentes podem marcar destinatários como aprovadores. Os destinatários marcados como aprovadores podem revisar e aprovar contratos, mas não precisam assiná-los. Os aprovadores podem ser solicitados a inserir dados em campos durante o processo de aprovação.
   * **ID de Pasta do Contrato Preferencial**: Usado para especificar a pasta onde os contratos assinados finais são armazenados. Se você não definir um valor para esse campo, os contratos assinados finais serão salvos na mesma pasta do arquivo de documento original por padrão. A ID da pasta deve ser um número.
   * **PDF de Transação de Anexação Automática**: Se ativado, os PDF de transação são anexados automaticamente aos contratos quando novos contratos são criados a partir de registros de transação.
   * **Adicionar PDF assinado como (anexo ou link)**: Se *Lista* for selecionado na lista suspensa, o PDF Assinado será adicionado automaticamente como um link para o arquivo. Se *Anexo* for selecionado na lista suspensa, a PDF assinada será armazenada em [!DNL NetSuite] como um anexo no registro do contrato.
   * **Incluir PDF de trilha de auditoria com o contrato**: Se estiver ativado, as PDF de trilha de auditoria são anexadas automaticamente aos registros do contrato após a assinatura dos contratos.
   * **Método de Verificação de Identidade Aplica-se a**: Ativar qualquer um dos métodos de verificação de identidade determina a quem o método de verificação de identidade é aplicado. As opções são *Todos os signatários, somente signatários externos* ou *Somente signatários internos*.

   **Métodos de verificação de identidade** {#identity-verification-methods}

   Os métodos de verificação de identidade ativados podem ser selecionados ao criar um contrato. Se mais de um método de verificação de identidade estiver ativado aqui, a página Contrato da Adobe Sign exibirá um **[!UICONTROL Verificar identidade do signatário]** opção.

   * **Ativar senha necessária para assinar**: Exigir que os signatários insiram uma senha única especificada.

   * **Ativar autenticação baseada em conhecimento**: Exigir que os signatários forneçam seu nome, endereço e, opcionalmente, os últimos quatro dígitos da SSN e respondam a uma lista de perguntas que verificam as informações fornecidas. Disponível apenas nos Estados Unidos.

   * **Ativar autenticação de identidade Web**: Exigir que os signatários verifiquem sua identidade fazendo logon em um dos seguintes sites: Facebook, Google, LinkedIn, Microsoft Live, Twitter ou Yahoo!.

   * **Provisionamento automático do usuário no Adobe Sign**: Se ativado, os usuários que enviam contratos [!DNL NetSuite] são provisionados automaticamente com uma conta de usuário da Adobe Sign.


1. Selecionar **[!UICONTROL Salvar]** para salvar suas preferências.

## Configurar atualizações automáticas de status {#asu}

O pacote de integração da Adobe Sign permite que você receba atualizações automaticamente no [!DNL NetSuite] sobre o status dos contratos enviados de [!DNL NetSuite]. Quando este recurso estiver ativado, [!DNL NetSuite] sempre reflete o status dos contratos. Você pode ativar as atualizações de status automáticas da seguinte maneira:

1. Navegue até **[!UICONTROL Configuração > Empresa > Ativar recursos].**
1. Selecione o **[!UICONTROL SuiteCloud]** subguia.
1. Ative as seguintes opções:

   * Na seção SuiteBuilder, ative **[!UICONTROL Registros personalizados]** opção.

   * Na seção SuiteScript, ative o **[!UICONTROL Client SuiteScript]** e **[!UICONTROL SuiteScript de servidor]** e concordar com os termos de serviço para ambos.

1. Selecionar **[!UICONTROL Salvar]**.

   Suas opções são definidas conforme mostrado na imagem.

   ![Ativar recursos da SuiteCloud](images/enable-suitecloudfeatures.png)

## Objetos e tipos de registro {#objects}

O pacote de integração da Adobe Sign já expõe o objeto Contrato da Adobe Sign com vários padrões [!DNL NetSuite] objetos, incluindo: Registros de Cliente, Estimativa, Lead, Oportunidade e Parceiro. Você também pode usar o pacote do Adobe Sign com outros tipos de registro, incluindo registros personalizados.

A guia Contrato pode ser exibida com dois tipos de [!DNL NetSuite] registros: Registros de entidade e transação. Geralmente presumimos que um registro de transação é um registro (como cota) que pode ser convertido em um documento de PDF. enquanto um registro da entidade não pode ser convertido em um PDF.

## Registros de transação {#transrecords}

Se o contrato for criado a partir de um registro de transação, o primeiro documento no registro do contrato será a versão PDF do registro de onde ele veio e o primeiro destinatário será o endereço de email do registro. Se você não deseja que o primeiro documento seja uma versão de PDF do registro de onde ele veio, vá para **[!UICONTROL Configuração > Empresa > Preferências gerais > subguia Preferências personalizadas]** e desativar **[!UICONTROL PDF de Transação de Anexação Automática]** opção. Consulte [Configuração de preferências personalizadas](#configure) para obter mais informações.

Em Preferências personalizadas, você também pode ativar o **[!UICONTROL Usar Trans. Contato como primeiro signatário]** se desejar que o contato principal da transação seja adicionado automaticamente como o primeiro signatário. Quando associado a um registro de Transação, ele exibe o **[!UICONTROL Contratos]** e **[!UICONTROL Send for Signature]** botões.

![Aspas](images/quote.png)

## Registros de entidade {#entity-records}

Se o contrato for criado a partir de um registro da entidade, o primeiro destinatário será o endereço de email do registro. Quando associada a um registro de Entidade, somente a guia Contratos é exibida.

## Personalizar o pacote {#customize}

Personalizar o pacote inclui o seguinte:

* Implantar os scripts para a subguia Contratos e o botão Send for Signature para os tipos de registro apropriados.
* Definindo permissões de função para seus tipos de registro Adobe Sign.
* Modificação de permissões para conceder acesso ao *Contratos* subguia e o *Send for Signature* botão.

![Scripts](images/scripts.png)

### Configurar contratos da Adobe Sign para tipos de registro adicionais  {#configuring-adobe-sign-agreements-for-additional-record-types}

Para implantar o *Contratos* subguia e o *Send for Signature* Botão para os tipos de registro adequados:

1. Navegue até **[!UICONTROL Personalização > Scripts > Scripts].**

1. No *Scripts* página de lista exibida, localize o script que você deve implantar e selecione ****[!UICONTROL Exibir]****.

   * Para adicionar o *Send for Signature* botão, selecione **[!UICONTROL Botão Estimativa do Adobe Sign]** script.

   * Para adicionar o *Contratos* guia, selecione **[!UICONTROL Carregador de contrato da Adobe Sign]** script.

1. Na página Script, selecione **[!UICONTROL Implantar script]**.

   ![Implantar script](images/deploly-script.png)

1. Na página Implantação de script, faça o seguinte:

   * Na *Aplica-se a* , selecione o tipo de registro.
   * Opcionalmente, insira a ID de implantação do script.

      Consulte o *Criando uma ID de Implantação de Script Personalizado* tópico no [!DNL NetSuite] Centro de ajuda para obter mais informações. Se você não inserir uma ID, uma será gerada.

   * Verifique a **[!UICONTROL Implantado]** caixa de seleção.

   ![Implantação de script](images/execute-as-admin.png)

   * Conjunto *Status* para **[!UICONTROL Lançado]**.

      Não é necessário especificar um *Tipo de evento* ou *Nível de registro*.

   * Na [!UICONTROL *Executar como função]* menu suspenso, selecione **[!UICONTROL Executar como administrador]**.

   * Com o **[!UICONTROL Público]** subguia ativa (ativa por padrão), selecione as funções específicas ou os usuários aos quais você deseja conceder acesso. Se você deseja conceder acesso a todas as funções e usuários, ative o respectivo **[!UICONTROL Selecionar tudo]** opções.

   * Selecionar **[!UICONTROL Salvar]**. Quando a confirmação de alteração for exibida, selecione **[!UICONTROL Voltar]**.


1. selecionar **[!UICONTROL Lista]** na parte superior da página Implantação de script para retornar ao *Scripts* página da lista.
1. Repita as etapas 2 e 3 acima para o outro script.

## Definir permissões de função para tipos de registro Adobe Sign {#setting-role-permissions-for-adobe-sign-record-types}

Mais [!DNL NetSuite] as funções devem ter permissão para usar o Adobe Sign sem personalização adicional. No entanto, você pode conceder permissões para quaisquer funções personalizadas adicionais que foram criadas.

1. Navegue até **[!UICONTROL Personalização > Listas, Registros e Arquivos > Tipos de registros]**.

   ![SiteBuilder - Registros personalizados](images/sitebuilder-customrecords.png)

   >[!NOTE]
   >
   >Se você não vir o *Tipos de registro* item, navegue até **[!UICONTROL Configuração > Empresa > Ativar recursos > guia Suite Cloud]** e ativar *Registros personalizados* opção.

1. No *Tipos de registro* página, selecione **[!UICONTROL Contrato Adobe Sign]** para selecioná-lo

   ![Tipos de registro de contrato](images/search-adobe-signagreementsforedit.png)

1. No *Tipo de registro personalizado* página, selecione **[!UICONTROL Usar lista de permissões]** do *Tipo de acesso* lista suspensa.

   ![Tipo de registro personalizado](images/custom-record-type.png)

   >[!NOTE]
   >
   >O *Contrato Adobe Sign* tipo de registro é o único tipo de registro Adobe Sign que exigiu o *Usa lista de permissões* tipo de acesso.
   >
   >
   >Consulte a etapa 6 para obter instruções sobre como definir o tipo de acesso para os outros tipos de registro da Adobe Sign.

1. Selecione o **[!UICONTROL Permissões]** subguia.

   A lista de funções e permissões é exibida.

   ![Funções e permissões](images/roles-and-permissions.png)

1. Defina as permissões da seguinte forma para as funções personalizadas adicionais adicionadas ao[!UICONTROL Contrato Adobe Sign]&quot; tipo de registro.

   >[!NOTE]
   >
   >Veja o *[Configurando uma Lista de Permissões para um Tipo de Registro Personalizado](https://system).[!DNL NetSuite]com/app/help/helpcenter.nl?fid=section_N2879931.html)* tópico no [!DNL NetSuite] Centro de ajuda para obter mais informações

   1. Selecione a função no *Função* lista.
   1. Conjunto *Nível* para **[!UICONTROL Total]**.
   1. Conjunto *Formulário padrão* para **[!UICONTROL Formulário de contrato personalizado do EchoSign]**.
   1. Selecionar **[!UICONTROL Restringir formulário]** caixa de seleção.
   1. Selecionar **[!UICONTROL Adicionar]** para salvar as alterações da linha de função.

   ![Definir permissões](images/set-permissions.png)

   A nova linha é exibida conforme mostrado abaixo:

   ![Definir permissões para o tipo de registro de contrato](images/set-permissions-foragreementrecordtype.png)

   Repita as etapas de a e acima para todas as funções personalizadas adicionais.

   * selecionar **[!UICONTROL Salvar]** no *Tipo de registro personalizado* quando as permissões de todas as funções foram definidas.
   O *[!UICONTROL Tipo de Registro do Cliente]* é exibida novamente.

1. Repita as etapas 1 a 3 acima para definir o *Tipo de acesso* para todos os outros tipos de registro da Adobe Sign

   **[!UICONTROL Nenhuma permissão necessária].** Isso se aplica aos seguintes tipos de registro:

   * Adobe Sign Config
   * Documento do Adobe Sign
   * Evento Adobe Sign
   * Idioma Adobe Sign
   * Erros de script Adobe Sign
   * Contrato assinado pela Adobe Sign
   * Signatário da Adobe Sign

### Conceder acesso à guia Contrato e ao botão Send for Signature  {#granting-access-to-the-agreement-tab-and-send-for-signature-button}

O pacote de integração da Adobe Sign já expõe o objeto Contrato da Adobe Sign com vários padrões [!DNL NetSuite] objetos (Cliente, Estimativa [Cota], Lead e muito mais). O *Contrato* a subguia é ativada automaticamente para os seguintes tipos de objetos: Cliente, Lead, Oportunidade, Parceiro, Cliente Potencial, Cota e Lista de Fornecedores.

O *[!UICONTROL Send for Signature]* botão é ativado automaticamente **o[!UICONTROL Somente para o objeto Cota]**.

[!DNL NetSuite] os administradores podem estender a capacidade de criar contratos para objetos adicionais do CRM modificando permissões para adicionar *Contrato* subguia, *Send for Signature* ou ambos os objetos.

#### Modificação de permissões para conceder acesso ao botão Send for Signature  {#modifying-permissions-to-grant-access-to-the-send-for-signature-button}

1. Navegue até **[!UICONTROL Personalização > Scripts > Scripts]**.

   O *Scripts* é exibida.

   * Se necessário, use os filtros para localizar os scripts Adobe Sign

1. No *Scripts* localize a *Botão Estimativa do Adobe Sign* script (controla o *Send for Signature* botão) e, em seguida, selecione **Exibir**.

   ![Botão Visualizar estimativas da Adobe Sign](images/view-adobe-sign-estimatesbutton.png)

1. No *Script* faça o seguinte:

   * selecione o **[!UICONTROL Implantações]** subguia

   * Em &quot;*Aplica-se a*&quot; selecione o link da entidade que deseja modificar.

      * **[!UICONTROL Cota]** neste exemplo

   ![selecione a subguia Implantações](images/click-the-deploymentssub-tab.png)

   * selecione o **[!UICONTROL Editar]** no botão *Implantação de script* página

   ![Editar implantação de script](images/edit-script-deployment.png)

   * Com o **[!UICONTROL Público]** na subguia ativa, selecione as funções específicas ou os usuários aos quais você deseja conceder acesso.

      * Se você deseja conceder acesso a todas as funções e usuários, ative o respectivo **[!UICONTROL Selecionar tudo]** opções
   * selecionar **[!UICONTROL Salvar]**

   ![Selecione as funções específicas](images/save-script-deployment-quote.png)

#### Modificação de permissões para conceder acesso à guia Contratos  {#modifying-permissions-to-grant-access-to-the-agreements-tab}

1. Navegue até **[!UICONTROL Personalização > Scripts > Scripts]**
1. No [!UICONTROL Scripts] localize a *[!UICONTROL Carregador de contrato da Adobe Sign]* script (controla o *Guia Contratos*) e selecione **[!UICONTROL Exibir]**.
1. No *Script* faça o seguinte:

   1. Selecione o **[!UICONTROL Implantações]** subguia
   1. Em &quot;*[!UICONTROL Aplica-se a]*&quot; selecione o link da entidade para a qual você deseja modificar o acesso
   1. No *[!UICONTROL Implantação de script]* selecione o **[!UICONTROL Editar]** botão
   1. Com o **[!UICONTROL Público]** subguia ativa (está ativa por padrão), selecione as funções específicas ou os usuários aos quais você deseja conceder acesso. Se você deseja conceder acesso a todas as funções e usuários, ative o respectivo **[!UICONTROL Selecionar tudo]** opções
   1. selecionar **[!UICONTROL Salvar]**

## Uso do Adobe Sign para [!DNL NetSuite] pacote

Para enviar contratos de [!DNL NetSuite] e receber atualizações sobre esses contratos, os usuários devem ter a mesma ID de logon (endereço de email) em [!DNL NetSuite] e no Adobe Sign.

### Criação de um contrato da Adobe Sign

Depois de instalar um novo pacote em uma conta Sandbox ou Production, você deve testar o pacote criando um novo contrato. Você pode criar contratos da Adobe Sign a partir de um registro de entidade, de um registro de transação ou como um contrato independente.

>[!NOTE]
>
>O processo de criação de um contrato varia um pouco dependendo de como ele é criado. O processo geral envolve especificar as opções do contrato, adicionar um ou mais documentos do contrato e especificar os destinatários. O processo descrito abaixo pressupõe que você esteja criando o contrato a partir de um registro de cliente.

1. Selecione ou crie um registro de cliente do qual você gostaria de enviar um contrato ou selecione outro [!DNL NetSuite] tipo de registro com a guia Contratos ativada.

1. No registro, selecione o **[!UICONTROL Contratos]** subguia.
1. Selecionar **[!UICONTROL Novo contrato]**.

   ![Novo contrato](images/new-agreement.png)

1. No *[!UICONTROL Contrato Adobe Sign]* página, selecione **[!UICONTROL Editar]**.

   ![Editar novo contrato](images/edit-new-agreement.png)

1. Especifique as opções do contrato da seguinte maneira:

   * **Nome do contrato** — Digite um nome para o contrato.
   * **Mensagem**-Insira uma mensagem personalizada para o destinatário.
   * **Tipo de assinatura** — Selecione o tipo de assinatura aceito para o documento. As opções são *assinatura eletrônica* e *Assinatura por fax*.

   * **Eu também devo assinar este contrato** — Ative esta opção para indicar que o remetente também precisa assinar o contrato.
   * **Ordem de assinatura**-Se o *Eu também devo assinar este contrato* estiver ativada, selecione a ordem na qual o remetente e os destinatários devem assinar. As opções são &quot;Eu assino, depois os destinatários assinam&quot;, &quot;Os destinatários assinam, depois eu assino&quot; e &quot;Nenhum&quot;.

   * **Visualizar assinaturas do documento ou posição (ou campos de formulário)** — Ative essa opção para permitir que os remetentes visualizem o contrato e para permitir que adicionem campos (arraste e solte a assinatura, campos iniciais e outros campos de formulário) ao contrato antes de enviá-lo aos destinatários.
   * **Verificar identidade do signatário** — Ative esta opção e selecione uma das seguintes opções de verificação de identidade

      * Essa opção é exibida somente quando mais de um dos três métodos de verificação de identidade de signatário listados abaixo está ativado em Preferências personalizadas. (Consulte [Definir preferências personalizadas](#customize) para obter mais informações.) Se apenas uma preferência estiver ativada, o **[!UICONTROL Verificar identidade do signatário]** não é exibida.

   **Métodos de verificação de identidade**

   * **Senha necessária para assinar** — Exigir que os signatários insiram uma senha única especificada.
   * **Autenticação baseada em conhecimento** — Exigir que os signatários forneçam seu nome, endereço e, opcionalmente, os últimos quatro dígitos da SSN e respondam a uma lista de perguntas que verificam as informações fornecidas. Disponível apenas nos Estados Unidos.
   * **Autenticação de identidade Web** — Exigir que os signatários verifiquem sua identidade fazendo logon em um dos seguintes sites: Facebook, Google, LinkedIn, Twitter, Yahoo! ou Microsoft Live.
   * **Senha necessária para exibir o PDF** — Ative esta opção para exigir que um destinatário insira uma senha antes de abrir um PDF do contrato ou do contrato assinado. O arquivo de PDF enviado a todos é criptografado e requer a senha para abri-lo. Não perca sua senha, pois ela não é recuperável. Caso perca a senha, você deve excluir essa transação e começar novamente.
   * **Senha/Confirmar Senha** — Se a *Senha necessária para exibir o PDF* estiver ativada, insira a senha que deve ser usada para exibir o contrato.
   * **Lembrar destinatários ao assinar** — Especifique se e com que frequência os lembretes são enviados aos destinatários. As opções são *Nunca*, *Diário* ou *Semanal*.
   * **Idioma:** Especifique o idioma no qual a página de assinatura e as notificações por email são exibidas para os destinatários.
   * **Hospedar assinatura para o primeiro signatário** — Ative essa opção para permitir que o remetente assine pessoalmente no host do remetente para o primeiro signatário.
   * **Dias até o prazo de assinatura** — Insira um número inteiro para indicar o prazo de assinatura do contrato (data de hoje + número de dias).
   * **Registro pai** — Opcionalmente, selecione um registro pai para vinculá-lo ao contrato.

   ![Configurar contrato](images/configure-agreement-2.png)

1. Selecione o **[!UICONTROL Documentos]** guia.

   ![Guia Documentos](images/documents-tab.png)

1. No *Documentos* subguia, anexe um documento existente do gabinete de arquivos usando o *Documento Adobe Sign* e selecione **[!UICONTROL Anexar]**.

   Ou, clique em **[!UICONTROL Novo documento da Adobe Sign]** para acessar *[!UICONTROL Documento Adobe Sign]* e digite o nome de um documento no [!DNL NetSuite] gabinete de arquivos, selecione arquivos do registro de transação (se aplicável) ou anexe um novo documento.

   Você pode adicionar vários documentos a um contrato.

1. Selecionar **[!UICONTROL Destinatários]** e especifique o destinatário selecionando na lista de contatos ou digitando um endereço de email.

   ![Adicionar destinatários](images/add-recipients.png)

   Cada um dos destinatários pode ser marcado como Signatário ou CC. Se a *Permitir a marcação de destinatários como signatários de aprovadores* a preferência personalizada está ativada, os destinatários também podem ser marcados como Aprovadores. Consulte [Definir preferências personalizadas](#customize) para obter mais informações.

   * **Signatários** deve assinar o contrato.
   * **Aprovadores** deve aprovar, mas não assinar o contrato e pode, opcionalmente, adicionar dados a um contrato.
   * **Destinatários do CC** são notificados sobre atualizações de contrato e quando o contrato é assinado e concluído. Os destinatários da CC não são parte do processo de assinatura ou aprovação.

      Se a *Usar Contato de Registro Pai como Signatário* a preferência personalizada é ativada sozinha ou em conjunto com o *Usar Trans. Contato como signatário* , o primeiro destinatário é o padrão, mas pode ser alterado.

1. Selecionar **[!UICONTROL Adicionar]** após inserir cada destinatário.

1. Selecionar **[!UICONTROL Salvar]** para salvar o contrato.

### Enviar contratos para assinatura

Quando o contrato estiver pronto para ser enviado, selecione o **[!UICONTROL Send for Signature]** botão.

* Se a *Visualizar documentos ou posicionar assinaturas* estiver ativada, clique em **[!UICONTROL Send for Signature]**. Na janela que é aberta, visualize o documento ou arraste os campos de formulário para o documento antes de enviá-lo. Selecionar **[!UICONTROL Enviar]** para enviar o contrato ao destinatário.

* Se a *[!UICONTROL Hospedar assinatura para primeiro signatário]* estiver ativada, clique em **[!UICONTROL Send for Signature]**. Na janela que é aberta, permita que o signatário assine o documento com o remetente presente.

   A *Hospedar assinatura para signatário atual* também é exibido ao lado do *Hospedar assinatura para primeiro signatário* , que pode ser acessado até que o documento seja assinado. Use este link para hospedar a assinatura do contrato para vários signatários ou reabrir a janela pop-up se ela tiver sido fechada acidentalmente.

Uma vez que o contrato é enviado, os destinatários recebem um email informando-os dos documentos que aguardam a assinatura.

Depois que os destinatários assinarem o documento, o remetente receberá uma notificação por email informando que o documento foi assinado.

#### Enviar de uma Cota

A Adobe Sign tem integração direta com as cotações em [!DNL NetSuite] para que um PDF da cota seja gerado automaticamente e anexado ao registro do contrato.

Ao exibir uma Cota, selecione **[!UICONTROL Send for Signature]**. Ele gera e exibe a cota anexada ao contrato. Você também pode adicionar o *Send for Signature* para outros tipos de registro de transação. Consulte [Objetos e tipos de registro](#objects) para obter mais informações.

![Cota - Send for Signature](images/quote-send-forsignature.png)

### Monitorar status e enviar lembretes

Depois de enviar um contrato:

* O status do documento é alterado para *Enviado para assinatura* na seção Detalhes do contrato
* O *Send for Signature* é substituído pelos seguintes três botões:

   * **Status da atualização** — Para atualizar manualmente o status se as atualizações de status não tiverem sido configuradas. Consulte [Configuração de atualizações automáticas de status](#asu) para obter mais informações.
   * **Enviar lembrete** — Para enviar um lembrete ao signatário atual.
   * **Cancelar contrato** — Para cancelar um contrato. Um contrato pode ser cancelado depois de enviado para uma assinatura se todos os destinatários ainda não tiverem assinado.

![Enviado para assinatura](images/out-for-signature.png)

Um novo *Eventos* subguia é exibida no registro do contrato, onde você pode controlar o status do contrato.

Você pode ver um histórico dos eventos do contrato, que inclui informações sobre quando o contrato foi enviado, exibido e assinado.

![Eventos de contrato assinados](images/agreement-events.png)

Após a assinatura do contrato:

* Seu status muda para *Assinado*.
* Você pode vincular novamente ao Registro pai deste contrato usando o link.
* Você pode usar os links &quot;baixar&quot; em Documento assinado e Trilha de auditoria para acessar esses documentos.
* Um *Documento assinado* é exibida em uma subguia para exibir miniaturas do documento assinado.

![Contrato assinado](images/signed-agreement.png)

>[!NOTE]
>
>Depois que um contrato é enviado para assinatura, você não pode editar o registro. Isto é para preservar o registro dos acontecimentos.

## Desinstale o pacote

Para desinstalar o pacote, siga as etapas fornecidas na [!DNL NetSuite] Ajuda. Veja o *[Desinstalação de um pacote](https://docs.oracle.com/cloud/latest/)[!DNL NetSuite]cs_gs/NSBDL/NSBDL.pdf)* tópico no [!DNL NetSuite] Centro de ajuda para obter mais informações.

Quando você desinstala o pacote, os contratos não assinados são excluídos. Os contratos assinados e seus arquivos de PDF de auditoria correspondentes não são afetados.

NÃO desinstale o pacote se você precisar manter seus contratos não assinados.

## Solução de problemas

### Determine o progresso da atualização

Se a atualização parecer estar demorando mais do que isso, você pode verificar a subguia Log de execução do script de Instalação de Pacote do Adobe Sign para determinar o progresso da atualização da seguinte maneira:

1. Navegue até **[!UICONTROL Personalização > Scripts > Scripts]**.
1. No [!UICONTROL Scripts] localize a *[!UICONTROL Instalação do pacote Adobe Sign]* script e, em seguida, selecione **[!UICONTROL Editar]**.
1. No [!UICONTROL Scripts] selecione o **Log de execução** subguia.
1. selecionar **Atualizar**.

   O Registro de execução é atualizado para refletir o status. O *Detalhes* exibe o progresso das atualizações dos contratos.

   ![Progresso da atualização](images/refresh-progress.png)

### Resolver problemas de token de acesso

Você pode encontrar uma mensagem &quot;O token de acesso fornecido é inválido ou expirou&quot; ao interagir com contratos.

Isso pode ocorrer pelas seguintes razões:

* O [!DNL NetSuite]/Administrador da Adobe Sign que configurou o OAuth revogou o token de acesso
* O token de acesso expirou porque nenhum contrato foi enviado de [!DNL NetSuite] nos últimos 60 dias
* O [!DNL NetSuite]/Administrador da Adobe Sign não concluiu com êxito a configuração inicial do OAuth

Para resolver esse problema, execute o processo de configuração do OAuth novamente. Consulte [Configuração do OAuth após a instalação ou atualização](#oauth) para obter mais informações.

![Token inválido](images/invalid-token.png)

### Resolver problemas de status do documento {#resolvestatus}

Se [atualizações automáticas de status](#asu) estiverem configurados, mas o status do contrato não estiver atualizando após o envio dos contratos, tente o seguinte:

1. Verifique o log de execução da implantação *Atualização externa da Adobe Sign* para ver se você está recebendo chamadas da Adobe Sign da seguinte maneira:

   1. Navegue até **[!UICONTROL Personalização > Script > Implantações de script]**
   1. No *Implantações de script* localize a *Atualização externa da Adobe Sign* script e, em seguida, selecione **[!UICONTROL Editar]**
      1. No *[!UICONTROL Implantação de script]* selecione o **[!UICONTROL Log de execução]** subguia.
      * Você deveria ver um *Registro de contrato atualizado* entrada para cada ID de contrato


1. Verifique o log de execução da implantação *Contratos de atualização da Adobe Sign* para ver se há erros como se segue:

   1. Navegue até **[!UICONTROL Personalização > Script > Implantações de script]**.
   1. No [!UICONTROL Implantações de script] localize a *[!UICONTROL Contratos de atualização da Adobe Sign]* com o[!UICONTROL Agendado]&quot; status e, em seguida, selecione **[!UICONTROL Editar]**.
   1. No [!UICONTROL Implantação de script] selecione o **[!UICONTROL Log de execução]** subguia.
   1. Abaixo [!UICONTROL Tipo], selecione **[!UICONTROL Erro]** para filtrar os resultados.

1. Por fim, verifique o log de execução do *Adobe Sign Manager* para erros seguindo as instruções na etapa 2 acima.

### Resolver erros de tipo MIME  {#resolving-mime-type-errors}

Se você receber um erro de tipo MIME ao enviar um contrato, isso pode ocorrer porque o nome no campo Nome do arquivo não corresponde ao nome do arquivo e à extensão do arquivo carregado. Se você deixar o campo Nome do arquivo em branco, ele será preenchido automaticamente com o nome de arquivo e a extensão corretos.

### Exibir logs de script {#viewing-script-logs}

Você também pode exibir os logs de execução de implantação para scripts que não estão relacionados a problemas de status do documento. Consulte [Resolvendo problemas de status do documento](#resolvestatus) para obter mais informações.

1. Navegue até **[!UICONTROL Personalização > Scripts > Scripts]**.

   O *Scripts* é exibida. Se necessário, use os filtros para localizar o script apropriado.

1. Selecionar **[!UICONTROL Exibir]** para o script correspondente.

1. Selecione o **[!UICONTROL Log de execução]** na página para exibir o registro de script.

## Suporte {#support}

Vá para o [Portal de suporte da Adobe Sign](https://adobe.com/go/adobesign-support-center_br) para acessar as perguntas frequentes, a documentação, os artigos da base de conhecimento ou entrar em contato com o Suporte da Adobe.
