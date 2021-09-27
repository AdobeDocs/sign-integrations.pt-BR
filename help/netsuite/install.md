---
title: Adobe Sign for NetSuite - Guia de instalação e personalização (v4.0.4)
description: 'Adobe Sign for NetSuite - Guia de instalação e personalização '
product: Adobe Sign
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
source-git-commit: 924813403d8e13f816347dd548a68a16d78d866e
workflow-type: tm+mt
source-wordcount: '4952'
ht-degree: 0%

---


# Guia de instalação e personalização do Adobe Sign for NetSuite (v4.0.4){#install-customize-netsuite}

## Visão geral {#overview}

O Adobe Sign para NetSuite fornece uma integração completa de eSignature com o NetSuite. Você pode usar o Adobe Sign para integração com o Netsuite para enviar contratos como contratos, cotas e outros documentos, que exigem assinaturas eletrônicas, para destinatários diretamente do NetSuite. Você pode criar e enviar contratos da Adobe Sign de registros de clientes, clientes potenciais, cotas e outros do NetSuite. A Adobe Sign atualiza o NetSuite com o status atual dos contratos e armazena os contratos com os registros associados do NetSuite depois que eles são totalmente executados. Você pode ver o histórico de todos os contratos enviados do NetSuite de dentro do produto.

Consulte as [Notas de versão do Adobe Sign for NetSuite](https://experienceleague.corp.adobe.com/docs/sign-integrations/using/netsuite/release-notes.html?lang=en) para obter mais informações.

## Instalar o pacote e configurar o OAuth {#install}

Somente um administrador do NetSuite pode instalar ou atualizar o pacote. Para configurar o OAuth, o administrador do NetSuite deve ter acesso de administrador ao Adobe Sign. Antes de instalar o pacote na sua conta de produção, você deve instalar e testar o pacote em uma conta Sandbox do NetSuite.

Consulte [Criar um contrato da Adobe Sign](#createagreement) para obter mais informações sobre testes.

>[!CAUTION]
>
>Os clientes que atualizam para a v4.0.4 NÃO devem remover a chave de API existente.
>
>Consulte [Definir preferências personalizadas](#configure) para obter mais informações sobre como a chave da API é usada.

### Instale o pacote pela primeira vez

1. Navegue até **Personalização > SuiteBundler > Pesquisar e instalar pacotes**.

1. Na página *Pesquisar e instalar pacotes*, digite **Adobe Sign** como palavra-chave e selecione **Pesquisar**.

1. Selecione o nome do pacote **Adobe Sign**.

   ![Procurar o pacote](images/search-for-the-bundle.png)

1. Na página *Detalhes do pacote*, selecione **Instalar**.
1. Na página *Instalar pacote de visualização*, selecione **Instalar pacote**.

   (Não é necessário alterar nenhum dos valores padrão na página)

   ![Instalar o pacote](images/bundle-details-install.png)

1. Na caixa de diálogo Instalar exibida, selecione **OK** para continuar.

   Durante o processo de instalação, o status do pacote é exibido como *Pendente*.

   ![Instalação de pacotes](images/installing-bundles.png)

1. Para exibir um status atualizado, selecione **Atualizar**.

   Após a conclusão da instalação do pacote, *Adobe Sign for NetSuite* é exibido na página *Pacotes Instalados*.

   ![Pacotes instalados](images/installed-bundles.png)

1. Se você já é uma conta de cliente da Adobe Sign, siga as etapas para [Configurar OAuth após instalar ou atualizar](#oauth).

   Se você não tiver uma conta da Adobe Sign, poderá [cadastrar-se em uma conta de avaliação corporativa](https://esign.adobe.com/adobe-sign-netsuite-trial-registration.html) para testar o sistema. Siga as etapas de registro online para ativar sua conta da Adobe Sign.

## Configurar o OAuth após a instalação ou atualização {#oauth}

A Adobe Sign usa o OAuth 2.0 para autenticar sua conta Adobe Sign no NetSuite.

Este protocolo autoriza seu pacote NetSuite instalado a se comunicar com a Adobe Sign sem solicitar sua senha. Já que informações confidenciais não está sendo compartilhadas diretamente entre os aplicativos, sua conta tem menos probabilidade de ficar comprometida.

Essa autenticação não afeta sua implementação, mas você deve fazer uma configuração única após instalar ou atualizar o pacote em sua conta de Produção ou Sandbox.

O administrador do NetSuite que configura o OAuth também deve ter um acesso de administrador no nível da conta ao Adobe Sign.

1. No NetSuite, navegue até a página de lista *Adobe Sign Config*.

1. Procure **Adobe Sign Config** (um tipo de registro personalizado) usando o campo Pesquisar no cabeçalho.

1. Na página Resultados da pesquisa, selecione **Exibir** para o registro *Adobe Sign Config*.

   ![Procure por Adobe Sign](images/search-for-adobesignconfig.png)

1. Na página Lista de configurações da Adobe Sign, selecione **Exibir** para o registro *Usando OAuth para acessar as APIs da Adobe Sign*.

   ![Lista de configurações da Adobe Sign](images/adobe-sign-configlist.png)

1. Na página Adobe Sign Config, selecione **Iniciar sessão com o Adobe Sign**

   ![Faça logon ](images/log-in-with-adobesign.png)

1. Na página de logon do Adobe Sign exibida, insira suas credenciais e selecione **Fazer logon**.

   ![autenticar no Adobe Sign](images/8-authenticate-toadobesign-2020.png)

1. Na página Confirmar Acesso (para OAuth) exibida, selecione **Permitir Acesso**

   ![Permitir acesso](images/confirm-access.png)

1. Quando a autorização estiver concluída, você será redirecionado de volta à página Adobe Sign Config no NetSuite, conforme mostrado abaixo.

   ![OAuth bem-sucedido](images/successful-oauth.png)

   >[!NOTE]
   >
   >Se você estiver configurando o OAuth na sua conta do Sandbox, ocorrerá o erro &quot;Não foi possível determinar a composição do cliente&quot; quando a autorização for concluída.
   >
   >
   >Para continuar, você deve alterar a parte do domínio da conta do URL (system.netsuite.com) em seu navegador para retornar à Sandbox do NetSuite da seguinte maneira:
   >
   >
   >Alterar:
   >
   >
   >system.netsuite.com/app/site/hosting/scriptlet.nl?script=745&amp;deploy=1&amp;web_access_point=https://echosign.com
   >
   >
   >Para:
   >
   >
   >sistema.**sandbox.**netsuite.com/app/site/hosting/scriptlet.nl?script=745&amp;deploy=1&amp;web_access_point=https://echosign.com

## Atualizar o pacote (usuários existentes)

As atualizações do pacote NetSuite são lançadas regularmente pelo Adobe. Os usuários existentes da integração do Adobe Sign para NetSuite podem atualizar para o pacote mais recente.

>[!CAUTION]
>
>Os clientes que atualizam para uma versão mais recente NÃO devem remover a chave de API existente.
>
>Consulte [Definir preferências personalizadas](#configure) para obter mais informações sobre como a chave da API é usada.

### Pré-requisitos {#prerequisites}


O tempo necessário para atualizar para o pacote v4.0.4 depende do número de contratos que têm o status &quot;Enviado para assinatura&quot;. Geralmente, leva de 7 a 10 minutos para atualizar 100 contratos. Anote o número de registros para estimar a hora da atualização.

Para determinar o número de contratos enviados para assinatura:

1. Navegue até **Personalização > Listas, Registros e Arquivos > Tipos de Registro** e localize *Contrato Adobe Sign.*

   Ou procure Contratos da Adobe Sign na barra de pesquisa.

1. Para o registro de Contratos da Adobe Sign, selecione **Pesquisar**.

   ![Pesquisar Tipos de Registro](images/search-adobe-signagreements.png)

1. Na lista suspensa **Status**, selecione **Enviado para assinatura** e selecione **Enviar**.

   ![Enviar para assinatura](images/submit-search-foragreements.png)

   Anote o número de registros para estimar a hora da atualização.

   ![Anote o número](images/search-results.png)

### Atualizar o pacote {#updating-the-bundle}

1. Navegue até **Personalização > SuiteBundler > Pesquisar e instalar > Lista** e localize seu pacote atual, conforme mostrado abaixo.

   >[!NOTE]
   >
   >Se houver uma nova versão do pacote, um ícone de ponto de exclamação será exibido à direita do número *Versão* do seu pacote atual.

1. No menu suspenso Ação, selecione **Atualizar**.

   ![Atualizar ação](images/update-action.png)

1. Na página Atualização do pacote de visualização, selecione **Atualizar pacote** sem alterar nenhum dos valores padrão exibidos na página.

   Durante a instalação, o status do pacote é exibido como *Pendente*.

   ![Atualização](images/preveiw-bundles-update.png) do pacote de visualização.

   >[!NOTE]
   >
   >Ao atualizar o pacote, você pode receber uma mensagem de aviso conforme mostrado abaixo. Se você não personalizou seus registros de assinatura eletrônica do NetSuite, pode continuar. Se não tiver certeza, é sugerido que você instale o pacote em uma conta Sandbox para testá-lo primeiro antes de atualizar o pacote em uma conta de produção.
   ![Mensagem de erro](images/netsuite-error.png)

1. Para exibir um status atualizado, selecione **Atualizar**.

   ![Instalação da atualização](images/installing-upgrade.png)

   >[!NOTE]
   >
   >Se a atualização parecer demorar porque você tem um grande número de contratos *Enviado para assinatura*, você pode verificar a subguia **Log de execução** do script *Instalação do pacote Adobe Sign* para determinar o progresso da atualização. (Consulte [Determinar o progresso da atualização](#determineprogress)para obter mais informações.)

   Após a conclusão da atualização do pacote, *Adobe Sign para NetSuite* é exibido na página *Pacotes Instalados*.

   ![Pacote instalado](images/4-installed-bundles.png)

## Configurar o pacote {#configure}

### Definir preferências personalizadas  {#set-custom-preferences}

Você pode usar preferências personalizadas para especificar como os contratos são criados e armazenados no NetSuite. Além disso, a preferência *Provisionar usuário automaticamente no Adobe Sign* permite especificar se os usuários do NetSuite serão provisionados automaticamente nos serviços do Sign quando enviarem contratos do NetSuite.

1. Navegue até **Configuração > Empresa > Preferências gerais**.
1. Role a página para baixo e selecione a subguia **Preferências personalizadas**.

   ![Preferências personalizadas](images/custom-preferences.png)

1. Ative e configure suas preferências do Adobe Sign conforme necessário:

   * **Digite a chave da API do EchoSign para sua conta**: Não adicione ou edite nenhum valor neste campo.
   * **Usar Contato de Registro Pai como Signatário**: Se ativado, o contato do registro pai é assumido como o primeiro signatário quando os contratos são criados. O remetente pode remover ou editar facilmente o signatário padrão ou adicionar outros signatários ao contrato antes de enviá-lo.
   * **Usar Trans. Entre em contato com o signatário se estiver presente**: Essa preferência é válida somente se a preferência *Usar contato de registro pai como signatário* também estiver ativada. Se ativado, ao gerar um contrato a partir de um Registro de transação (por exemplo, Cota), o contato principal da transação é assumido como padrão como o primeiro signatário. (Consulte [Registros de Transação](#transrecords)para obter mais informações.) Se não houver contato principal de transação, ou se estiver enviando do registro de objeto do NetSuite (por exemplo, registro de cliente, registro de parceiro), o destinatário padrão será o contato principal para o email do cliente. O remetente pode remover ou editar facilmente o signatário padrão ou adicionar outros signatários ao contrato antes de enviá-lo.
   * **Permitir a marcação de destinatários como aprovadores**: Se ativado, os remetentes podem marcar destinatários como aprovadores. Os destinatários marcados como aprovadores podem revisar e aprovar contratos, mas não precisam assiná-los. Os aprovadores podem ser solicitados a inserir dados em campos durante o processo de aprovação.
   * **Id** De Pasta De Contrato Preferencial: Usado para especificar a pasta onde os contratos assinados finais serão armazenados. Se você não definir um valor para esse campo, os contratos assinados finais serão salvos na mesma pasta do arquivo de documento original por padrão. A ID da pasta deve ser um número.
   * **Anexar PDF** da transação automaticamente: Se ativado, os PDFs de transação são anexados automaticamente aos contratos quando novos contratos são criados a partir de registros de transação.
   * **Adicionar PDF assinado como (anexo ou link)**: Se a opção  ** Lista estiver selecionada na lista suspensa, o PDF assinado será adicionado automaticamente como um link para o arquivo. Se *Anexo* for selecionado na lista suspensa, o PDF assinado será armazenado no NetSuite como um anexo no registro do Contrato.
   * **Incluir PDF da trilha de auditoria com o contrato**: Se ativado, os PDFs de trilha de auditoria são anexados automaticamente aos registros do contrato depois que os contratos são assinados.
   * **Método de verificação de identidade Aplica-se a**: Ativar qualquer um dos métodos de verificação de identidade determina a quem o método de verificação de identidade é aplicado. As opções são *Todos os signatários, Somente signatários externos, *ou *Somente signatários internos*.

   **Métodos de verificação de identidade** {#identity-verification-methods}

   Os métodos de verificação de identidade ativados podem ser selecionados ao criar um contrato. Se mais de um método de verificação de identidade estiver ativado aqui, a página Contrato da Adobe Sign exibe uma opção **Verificar identidade do signatário**.

   * **Ativar senha necessária para assinar**: Exigir que os signatários insiram uma senha única especificada.

   * **Ativar autenticação** baseada em conhecimento: Exigir que os signatários forneçam seu nome, endereço e, opcionalmente, os últimos quatro dígitos da SSN e respondam a uma lista de perguntas que verificam as informações fornecidas. Disponível apenas nos Estados Unidos.

   * **Ativar autenticação** de identidade Web: Exigir que os signatários verifiquem sua identidade fazendo logon em um dos seguintes sites: Facebook, Google, LinkedIn, Microsoft Live, Twitter ou Yahoo!.

   * **Provisionamento automático do usuário no Adobe Sign**: Se ativado, os usuários que enviam contratos no NetSuite são provisionados automaticamente com uma conta de usuário da Adobe Sign.


1. Selecione **Salvar** para salvar suas preferências.

## Configurar atualizações automáticas de status {#asu}

O pacote de integração da Adobe Sign permite que você receba atualizações automaticamente no NetSuite em relação ao status dos contratos que foram enviados do NetSuite. Quando esse recurso é ativado, o NetSuite sempre reflete o status atual de seus contratos. Você pode ativar as atualizações de status automáticas da seguinte maneira:

1. Navegue até **Configuração > Empresa > Ativar Recursos.**
1. Selecione a subguia **SuiteCloud**.
1. Ative as seguintes opções:

   * Na seção SuiteBuilder, ative a opção **Registros personalizados**.

   * Na seção SuiteScript, ative as opções **Client SuiteScript** e **Server SuiteScript** e concorde com os termos de serviço para ambos.

1. Selecione **Salvar**.

   Suas opções são definidas conforme mostrado na imagem.

   ![Ativar recursos da SuiteCloud](images/enable-suitecloudfeatures.png)

## Objetos e tipos de registro {#objects}

O pacote de integração da Adobe Sign já expõe o objeto Contrato da Adobe Sign com muitos objetos padrão do NetSuite, incluindo: Registros de Cliente, Estimativa, Lead, Oportunidade e Parceiro. Você também pode usar o pacote do Adobe Sign com outros tipos de registro, incluindo registros personalizados.

A guia Contrato pode ser exibida com dois tipos de registros do NetSuite: Registros de entidade e transação. Geralmente presumimos que um registro de transação é um registro (como cota) que pode ser convertido em um documento PDF. enquanto um registro da entidade não pode ser convertido em um PDF.

## Registros de transação {#transrecords}

Se o contrato for criado a partir de um registro de transação, o primeiro documento no registro do contrato será a versão em PDF do registro de origem e o primeiro destinatário será o endereço de email do registro. Se não quiser que o primeiro documento seja uma versão em PDF do registro de onde veio, acesse **Configuração > Empresa > Preferências gerais > subguia Preferências personalizadas** e desative a opção **Anexar transação automaticamente PDF**. Consulte [Configurando preferências personalizadas](#configure) para obter mais informações.

Em Preferências personalizadas, você também pode ativar **Usar Trans. Entre em contato com a preferência Primeiro signatário** se quiser que o contato principal da transação seja adicionado automaticamente como o primeiro signatário. Quando associado a um registro de Transação, ele exibe os botões **Contratos** e **Send for Signature**.

![Aspas](images/quote.png)

## Registros de entidade {#entity-records}

Se o contrato for criado a partir de um registro da entidade, o primeiro destinatário será o endereço de email do registro. Quando associada a um registro de Entidade, somente a guia Contratos é exibida.

## Personalizar o pacote {#customize}

Personalizar o pacote inclui o seguinte:

* Implantar os scripts para a subguia Contratos e o botão Send for Signature para os tipos de registro apropriados.
* Definindo permissões de função para seus tipos de registro Adobe Sign.
* Modificando permissões para conceder acesso à subguia *Contratos* e ao botão *Send for Signature*.

![Scripts](images/scripts.png)

### Configurar contratos da Adobe Sign para tipos de registro adicionais  {#configuring-adobe-sign-agreements-for-additional-record-types}

Para implantar a subguia *Contratos* e o botão *Send for Signature* para os tipos de registro apropriados:

1. Navegue até **Personalização > Scripts > Scripts.**

1. Na página de lista *Scripts* exibida, localize o script que você precisa implantar e selecione **Exibir**.

   * Para adicionar o botão *Send for Signature*, selecione o script **Botão Estimativa do Adobe Sign**.

   * Para adicionar a guia *Contratos*, selecione o script **Carregador de Contrato da Adobe Sign**.

1. Na página Script, selecione **Implantar script**.

   ![Implantar script](images/deploly-script.png)

1. Na página Implantação de script, faça o seguinte:

   * Na lista *Aplica-se a*, selecione o tipo de registro.
   * Opcionalmente, insira a ID de implantação do script.

      Consulte o tópico *Criando uma ID de Implantação de Script Personalizado* no Centro de Ajuda do NetSuite para obter mais informações. Se você não inserir uma ID, uma será gerada.

   * Marque a caixa de seleção **Implantado**.

   ![Implantação de script](images/execute-as-admin.png)

   * Defina *Status* como **Liberado**.

      Não é necessário especificar um *Tipo de Evento* ou *Nível de Log*.

   * No menu suspenso *Executar como função*, selecione **Executar como administrador**.

   * Com a subguia **Público** ativa (ativa por padrão), selecione as funções ou usuários específicos aos quais você deseja conceder acesso. Se você deseja conceder acesso a todas as funções e usuários, ative as respectivas opções **Selecione todas**.

   * Selecione **Salvar**. Quando a confirmação de alteração for exibida, selecione **Voltar**.


1. selecione **Lista** na parte superior da página Implantação de Script para voltar à página de lista *Scripts*.
1. Repita as etapas 2 e 3 acima para o outro script.

## Definir permissões de função para tipos de registro Adobe Sign  {#setting-role-permissions-for-adobe-sign-record-types}

A maioria das funções do NetSuite deve ter permissão para usar o Adobe Sign sem personalização adicional. No entanto, talvez seja necessário conceder permissões para quaisquer funções personalizadas adicionais que tenham sido criadas.

1. Navegue até **Personalização > Listas, Registros e Arquivos > Tipos de Registros**.

   ![SiteBuilder - Registros personalizados](images/sitebuilder-customrecords.png)

   >[!NOTE]
   >
   >Se você não vir o item *Tipos de registro*, navegue até **Configuração > Empresa > Ativar recursos > guia Creative Cloud** e ative a opção *Registros personalizados*.

1. Na página *Tipos de Registro*, selecione **Contrato Adobe Sign** para selecioná-lo

   ![Tipos de registro de contrato](images/search-adobe-signagreementsforedit.png)

1. Na página *Tipo de registro personalizado*, selecione **Usar lista de permissões** no menu suspenso *Tipo de acesso*.

   ![Tipo de registro personalizado](images/custom-record-type.png)

   >[!NOTE]
   >
   >O tipo de registro *Adobe Sign Agreement* é o único tipo de registro Adobe Sign que requer o tipo de acesso *Usa a Lista de Permissões*.
   >
   >
   >Consulte a etapa 6 para obter instruções sobre como definir o tipo de acesso para os outros tipos de registro da Adobe Sign.

1. Selecione a subguia **Permissões**.

   A lista de funções e permissões é exibida.

   ![Funções e permissões](images/roles-and-permissions.png)

1. Defina as permissões da seguinte forma para as funções personalizadas adicionais adicionadas ao tipo de registro &quot;Contrato Adobe Sign&quot;.

   >[!NOTE]
   >
   >Consulte o tópico *[Configurando uma Lista de Permissões para um Tipo de Registro Personalizado](https://system.netsuite.com/app/help/helpcenter.nl?fid=section_N2879931.html)* no Centro de Ajuda do NetSuite para obter mais informações

   1. Selecione a função na lista *Função*.
   1. Defina *Level* como **Full**
   1. Defina *Formulário Predefinido* para **Formulário de Contrato EchoSign Personalizado**
   1. selecione para marcar a caixa de seleção *Restringir formulário*
   1. selecione **Adicionar** para guardar as alterações da linha de função

   ![Definir permissões](images/set-permissions.png)

   A nova linha é exibida conforme mostrado abaixo:

   ![Definir permissões para o tipo de registro de contrato](images/set-permissions-foragreementrecordtype.png)

   Repita as etapas de a e acima para todas as funções personalizadas adicionais.

   * selecione **Salvar** na página *Tipo de registro personalizado* quando as permissões para todas as funções tiverem sido definidas.

   A página *Tipo de Registro do Cliente* é exibida novamente.

1. Repita as etapas 1 a 3 acima para definir o *Tipo de acesso* para todos os outros tipos de registro Adobe Sign como

   **Nenhuma permissão necessária.** Isso se aplica aos seguintes tipos de registro:

   * Adobe Sign Config
   * Documento do Adobe Sign
   * Evento Adobe Sign
   * Idioma Adobe Sign
   * Erros de script Adobe Sign
   * Contrato assinado pela Adobe Sign
   * Signatário da Adobe Sign

### Conceder acesso à guia Contrato e ao botão Send for Signature  {#granting-access-to-the-agreement-tab-and-send-for-signature-button}

O pacote de integração da Adobe Sign já expõe o objeto Contrato da Adobe Sign com muitos objetos padrão do NetSuite (Cliente, Estimativa [Cota], Lead etc.). A subguia *Contrato* é ativada automaticamente para os seguintes tipos de objetos: Cliente, Lead, Oportunidade, Parceiro, Cliente Potencial, Cota e Lista de Fornecedores.

O botão *Send for Signature* é automaticamente ativado **apenas para o objeto Cota**.

Os administradores do NetSuite podem estender a capacidade de criar contratos para objetos adicionais do CRM modificando permissões para adicionar a subguia *Contrato*, o botão *Send for Signature* ou ambos a esses objetos.

#### Modificação de permissões para conceder acesso ao botão Send for Signature  {#modifying-permissions-to-grant-access-to-the-send-for-signature-button}

1. Navegue até **Personalização > Scripts > Scripts**.

   A página de lista *Scripts* é exibida.

   * Se necessário, use os filtros para localizar os scripts Adobe Sign

1. Na página *Scripts*, localize o script *Botão de Estimativa da Adobe Sign* (controla o botão *Send for Signature*) e selecione **Ver**.

   ![Botão Visualizar estimativas da Adobe Sign](images/view-adobe-sign-estimatesbutton.png)

1. Na página *Script*, faça o seguinte:

   * selecione a subguia **Implantações**

   * Em &quot;*Aplica-se a*&quot;, selecione o link da entidade que você deseja modificar

      * **** Cite este exemplo

   ![selecione a subguia Implantações](images/click-the-deploymentssub-tab.png)

   * selecione o botão **Editar** na página *Implantação de Script*

   ![Editar implantação de script](images/edit-script-deployment.png)

   * Com a subguia **Público** ativa, selecione as funções ou usuários específicos aos quais você deseja conceder acesso.

      * Se você deseja conceder acesso a todas as funções e usuários, ative as respectivas opções **Selecionar tudo**
   * selecione **Salvar**

   ![Selecione as funções específicas](images/save-script-deployment-quote.png)

#### Modificação de permissões para conceder acesso à guia Contratos  {#modifying-permissions-to-grant-access-to-the-agreements-tab}

1. Navegue até **Personalização > Scripts > Scripts**
1. Na página *Scripts*, localize o script *Adobe Sign Agreement Loader* (controla a *guia Contratos*)

   * selecione **Ver**

1. Na página *Script*, faça o seguinte:

   1. selecione a subguia **Implantações**
   1. Em &quot;*Aplica-se a*&quot;, selecione o link da entidade para a qual você deseja modificar o acesso
   1. Na página *Implantação de script, selecione o botão **Editar**

   1. Com a subguia **Público** ativa (está ativa por padrão), selecione as funções ou usuários específicos aos quais você deseja conceder acesso. Se você deseja conceder acesso a todas as funções e usuários, ative as respectivas opções **Selecionar tudo**

   1. selecione **Salvar**

## Uso do pacote Adobe Sign for NetSuite

Para enviar contratos do NetSuite e receber atualizações sobre esses contratos, os usuários devem ter a mesma ID de logon (endereço de email) no NetSuite e no Adobe Sign.

### Criação de um contrato da Adobe Sign

Depois de instalar um novo pacote em uma conta Sandbox ou Production, você deve testar o pacote criando um novo contrato. Você pode criar contratos da Adobe Sign a partir de um registro de entidade, de um registro de transação ou como um contrato independente.

>[!NOTE]
>
>O processo de criação de um contrato varia um pouco dependendo de como ele é criado. O processo geral envolve especificar as opções do contrato, adicionar um ou mais documentos do contrato e especificar os destinatários. O processo descrito abaixo pressupõe que você esteja criando o contrato a partir de um registro de cliente.

1. Selecione ou crie um registro de cliente do qual você gostaria de enviar um contrato ou selecione outro tipo de registro NetSuite que tenha a guia Contratos ativada.

1. No registro, selecione a subguia **Contratos**.
1. selecione **Novo contrato**.

   ![Novo contrato](images/new-agreement.png)

1. Na página *Adobe Sign Agreement*, selecione **Editar**.

   ![Editar novo contrato](images/edit-new-agreement.png)

1. Especifique as opções do contrato da seguinte maneira:

   * **Nome**  do contrato— Digite um nome para o contrato.
   * **Mensagem** - Insira uma mensagem personalizada para o destinatário.
   * **Tipo**  de assinatura— Selecione o tipo de assinatura aceito para o documento. As opções são *Assinatura eletrônica* e *Assinatura de fax*.

   * **Eu também preciso assinar este contrato** . Ative esta opção para indicar que o remetente também precisa assinar o contrato.
   * **Ordem** de assinatura - Se a opção  *Eu também preciso assinar este* contrato estiver ativada, selecione a ordem na qual o remetente e os destinatários devem assinar. As opções são &quot;Eu assino, depois os destinatários assinam&quot;, &quot;Os destinatários assinam, depois eu assino&quot; e &quot;Nenhum&quot;.

   * **Visualizar assinaturas do documento ou posição (ou campos de formulário)** — Ative essa opção para permitir que os remetentes visualizem o contrato e para permitir que adicionem campos (arraste e solte a assinatura, campos iniciais e outros campos de formulário) ao contrato antes de enviá-lo aos destinatários.
   * **Verificar a identidade**  do signatário— Ative esta opção e selecione uma das seguintes opções de verificação de identidade

      * Essa opção é exibida somente quando mais de um dos três métodos de verificação de identidade de signatário listados abaixo está ativado em Preferências personalizadas. (Consulte [Definir preferências personalizadas](#customize) para obter mais informações.) Se apenas uma preferência estiver ativada, a opção **Verificar identidade do signatário** não será exibida.

   **Métodos de verificação de identidade**

   * **Senha necessária para assinar** — Exigir que os signatários insiram uma senha única especificada.
   * **Autenticação**  baseada em conhecimento— Exigir que os signatários forneçam seu nome, endereço e, opcionalmente, os últimos quatro dígitos da SSN e respondam a uma lista de perguntas que verificam as informações fornecidas. Disponível apenas nos Estados Unidos.
   * **Autenticação**  de identidade Web— Exigir que os signatários verifiquem sua identidade fazendo logon em um dos seguintes sites: Facebook, Google, LinkedIn, Twitter, Yahoo! ou Microsoft Live.
   * **Senha necessária para exibir o PDF** — Ative esta opção para exigir que um destinatário insira uma senha antes de abrir um PDF do contrato ou do contrato assinado. O arquivo PDF enviado a todos será criptografado e essa senha será necessária para abri-lo. Não perca sua senha, pois ela não é recuperável. Caso perca a senha, será necessário excluir essa transação e começar novamente.
   * **Senha/Confirmar Senha** — Se a  *opção Senha necessária para exibir o* PDF estiver ativada, insira a senha que deve ser usada para exibir o contrato.
   * **Lembrar destinatários de assinar** — Especifique se e com que frequência os lembretes são enviados aos destinatários. As opções são *Nunca*, *Diário* ou *Semanal*.
   * **Idioma:** especifique o idioma no qual a página de assinatura e as notificações por email serão exibidas para os destinatários.
   * **Hospedar assinatura para o primeiro signatário** — Ative essa opção para permitir que o remetente assine pessoalmente no host do remetente para o primeiro signatário.
   * **Dias até o prazo**  de assinatura Insira um número inteiro para indicar o prazo de assinatura do contrato (data de hoje + número de dias).
   * **Registro**  principal— Opcionalmente, selecione um registro pai para vinculá-lo ao contrato.

   ![Configurar contrato](images/configure-agreement-2.png)

1. Selecione a guia **Documentos**.

   ![Guia Documentos](images/documents-tab.png)

1. Na subguia *Documents*, anexe um documento existente do gabinete de arquivos usando a lista suspensa *Documento da Adobe Sign* e selecione **Anexar**.

   Ou, clique em **Novo documento da Adobe Sign** para acessar a página *Documento da Adobe Sign* e digite o nome de um documento no gabinete de arquivos do NetSuite, selecione os arquivos do registro Transação (se aplicável) ou anexe um novo documento.

   Você pode adicionar vários documentos a um contrato.

1. Selecione a subguia **Destinatários** e especifique o destinatário selecionando na lista de contatos ou digitando um endereço de email.

   ![Adicionar destinatários](images/add-recipients.png)

   Cada um dos destinatários pode ser marcado como Signatário ou CC. Se a preferência personalizada *Permitir a marcação de destinatários como aprovadores signatários* estiver ativada, os destinatários também poderão ser marcados como aprovadores. Consulte [Definir preferências personalizadas](#customize) para obter mais informações.

   * **Os** signatários devem assinar o contrato.
   * **Os** aprovadores devem aprovar, mas não assinar o contrato, e podem, opcionalmente, precisar adicionar dados a um contrato.
   * **Os** destinatários da CC são notificados sobre atualizações de contrato e quando o contrato é assinado e concluído. Os destinatários da CC não são parte do processo de assinatura ou aprovação.

      Se a preferência personalizada *Usar Contato de Registro Pai como Signatário* estiver ativada sozinha ou em conjunto com a *Usar Trans. Entre em contato com a preferência Signatário*, o primeiro destinatário é o padrão, mas pode ser alterado.

1. Selecione **Adicionar** depois de inserir cada destinatário.

1. Selecione **Salvar** para salvar o contrato.

### Enviar contratos para assinatura

Quando o contrato estiver pronto para ser enviado, selecione o botão **Send for Signature**.

* Se a opção *Visualizar documento ou posicionar assinaturas* estiver ativada, clique em **Send for Signature**. Na janela que é aberta, visualize o documento ou arraste os campos de formulário para o documento antes de enviá-lo. Selecione **Enviar** para enviar o contrato ao destinatário.

* Se a opção *Assinatura do host para o primeiro signatário* estiver ativada, clique em **Send for Signature**. Na janela que é aberta, permita que o signatário assine o documento com o remetente presente.

   Um link *Assinatura de host para signatário atual* também é exibido ao lado do campo *Assinatura de host para primeiro signatário*, que pode ser acessado até que o documento seja assinado. Use este link para hospedar a assinatura do contrato para vários signatários ou reabrir a janela pop-up se ela tiver sido fechada acidentalmente.

Uma vez que o contrato é enviado, os destinatários recebem um email informando-os dos documentos que aguardam a assinatura.

Depois que os destinatários assinarem o documento, o remetente receberá uma notificação por email informando que o documento foi assinado.

#### Enviar de uma Cota

A Adobe Sign tem uma integração direta com as cotas no NetSuite para que um PDF da cota seja gerado automaticamente e anexado ao registro do contrato.

Ao exibir uma Cota, selecione **Send for Signature**. Ele gera e exibe a cota anexada ao contrato. Você também pode adicionar o botão *Send for Signature* a outros tipos de registro de transação. Consulte [Objetos e tipos de registro](#objects)para obter mais informações.

![Cota - Send for Signature](images/quote-send-forsignature.png)

### Monitorar status e enviar lembretes

Depois de enviar um contrato:

* O status do documento é alterado para *Enviado para assinatura* na seção Detalhes do contrato
* O botão *Send for Signature* é substituído pelos seguintes três botões:

   * **Atualizar status** — Selecione este botão para atualizar manualmente o status se as atualizações de status não tiverem sido configuradas. Consulte [Configurando atualizações automáticas de status](#asu)para obter mais informações.
   * **Enviar lembrete** — Selecione esse botão para enviar um lembrete ao signatário atual.
   * **Cancelar contrato** — Selecione este botão para cancelar um contrato. Um contrato pode ser cancelado depois de enviado para uma assinatura se todos os destinatários ainda não tiverem assinado.

![Enviado para assinatura](images/out-for-signature.png)

Uma nova subguia *Eventos* é exibida no registro do contrato, onde você pode controlar o status do contrato.

Você pode ver um histórico dos eventos do contrato, que inclui informações sobre quando o contrato foi enviado, exibido e assinado.

![Eventos de contrato assinados](images/agreement-events.png)

Após a assinatura do contrato:

* Seu status é alterado para *Assinado*.
* Você pode vincular novamente ao Registro pai deste contrato usando o link.
* Você pode usar os links &quot;baixar&quot; em Documento assinado e Trilha de auditoria para acessar esses documentos.
* Uma subguia adicional *Documento assinado* é exibida para exibir miniaturas do documento assinado.

![Contrato assinado](images/signed-agreement.png)

>[!NOTE]
>
>Depois que um contrato for enviado para assinatura, você não poderá editar o registro. Isto é para preservar o registro dos acontecimentos.

## Desinstale o pacote

Para desinstalar o pacote, siga as etapas fornecidas na Ajuda do NetSuite. Consulte o tópico *[Desinstalação de um pacote](https://docs.oracle.com/cloud/latest/netsuitecs_gs/NSBDL/NSBDL.pdf)* no Centro de Ajuda do NetSuite para obter mais informações.

Quando você desinstala o pacote, os contratos não assinados são excluídos. Os contratos assinados e seus arquivos PDF de auditoria correspondentes não são afetados.

NÃO desinstale o pacote se precisar manter seus contratos não assinados.

## Solução de problemas

### Determine o progresso da atualização

Se a atualização parecer estar demorando mais do que isso, você pode verificar a subguia Log de execução do script de Instalação de Pacote do Adobe Sign para determinar o progresso da atualização da seguinte maneira:

1. Navegue até **Personalização > Scripts > Scripts**.
1. Na página *Scripts*, localize o script *Instalação do pacote da Adobe Sign* e selecione **Editar**.
1. Na página *Script*, selecione a subguia **Log de Execução**.
1. selecione **Atualizar**.

   O Registro de Execução é atualizado para refletir o status atual. A coluna *Detalhes* exibe o progresso das atualizações dos contratos.

   ![Progresso da atualização](images/refresh-progress.png)

### Resolver problemas de token de acesso

Você pode encontrar uma mensagem &quot;O token de acesso fornecido é inválido ou expirou&quot; ao interagir com contratos.

Isso pode ocorrer pelas seguintes razões:

* O administrador do NetSuite/Adobe Sign que configurou o OAuth revogou o token de acesso
* O token de acesso expirou porque nenhum contrato foi enviado do NetSuite nos últimos 60 dias
* O administrador do NetSuite/Adobe Sign não concluiu com êxito a configuração inicial do OAuth

Para resolver esse problema, execute o processo de configuração do OAuth novamente. Consulte [Configurando o OAuth após instalar ou atualizar](#oauth) para obter mais informações.

![Token inválido](images/invalid-token.png)

### Resolver problemas de status do documento {#resolvestatus}

Se [atualizações automáticas de status](#asu) estiverem configuradas, mas o status do contrato não estiver sendo atualizado após o envio de contratos, tente o seguinte:

1. Verifique o log de execução da implantação do script *Adobe Sign External Update* para ver se você está recebendo chamadas da Adobe Sign da seguinte maneira:

   1. Navegue até **Personalização > Scripts > Implantações de Script**
   1. Na página *Implantações de Script*, localize o script *Adobe Sign External Update* e selecione **Editar**
      1. Na página *Implantação de Script*, selecione a subguia **Log de Execução**.
      * Você deve ver uma entrada *Registro de contrato atualizado* para cada ID de contrato


1. Verifique o log de execução da implantação do script *Adobe Sign Update Agreements* para ver se há algum erro da seguinte maneira:

   1. Navegue até **Personalização > Scripts > Implantações de Script**.
   1. Na página *Implantações de Script*, localize o script *Adobe Sign Update Agreements* com o status &quot;Agendado&quot; e selecione **Editar**.
   1. Na página *Implantação de Script*, selecione a subguia **Log de Execução**.
   1. Em *Tipo*, selecione **Erro** para filtrar os resultados.

1. Por fim, verifique se há erros no script *Adobe Sign Manager* no registro de execução seguindo as instruções da etapa 2 acima.

### Resolver erros de tipo MIME  {#resolving-mime-type-errors}

Se você receber um erro de tipo MIME ao enviar um contrato, isso pode ocorrer porque o nome no campo Nome do arquivo não corresponde ao nome do arquivo e à extensão do arquivo carregado. Se você deixar o campo Nome do arquivo em branco, ele será preenchido automaticamente com o nome de arquivo e a extensão corretos.

### Exibir logs de script {#viewing-script-logs}

Você também pode exibir os logs de execução de implantação para scripts que não estão relacionados a problemas de status do documento. Consulte [Resolução de problemas de status do documento](#resolvestatus)para obter mais informações.

1. Navegue até **Personalização > Scripts > Scripts**.

   A página de lista *Scripts* é exibida. Se necessário, use os filtros para localizar o script apropriado.

1. Selecione **Ver** para o script correspondente.

1. Selecione a subguia **Log de Execução** na página para exibir o log de script.

## Suporte {#support}

Acesse o [portal de suporte da Adobe Sign](https://adobe.com/go/adobesign-support-center_br) para acessar as perguntas frequentes, a documentação, os artigos da base de conhecimento ou para entrar em contato com o Suporte da Adobe.
