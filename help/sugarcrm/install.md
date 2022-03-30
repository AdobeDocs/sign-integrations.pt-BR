---
title: Adobe EchoSign para SugarCRM
description: Guia de instalação para habilitar a integração do Adobe Sign com o SugarCRM
product: Adobe Sign
content-type: reference
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 0512f616-568a-4b96-9bd1-48e67bc3536b
source-git-commit: 4d73ff36408283805386bd3266b683bc187d6031
workflow-type: tm+mt
source-wordcount: '2354'
ht-degree: 1%

---


# [!DNL SugarCRM] Guia de instalação {#sugarcrm-install-guide}

[Entre em contato com o Atendimento ao cliente](https://adobe.com/go/adobesign-support-center_br)

Adobe [!DNL EchoSign] para [!DNL SugarCRM] é a principal solução de contratos online eSignature que proporciona automação de assinaturas eletrônicas em [!DNL SugarCRM] para assinaturas eletrônicas e por fax. Os usuários podem enviar contratos diretamente do SugarCRM, exibir o histórico de contratos e salvar contratos assinados eletronicamente com contas, contatos, cotações associados e muito mais.
Adobe [!DNL EchoSign] para [!DNL SugarCRM] está disponível para todas as versões suportadas do SugarCRM, incluindo 6.3 - 6.7 para soluções sob demanda ou no local.

Este documento é um guia para [!DNL SugarCRM] administradores para saber como instalar e configurar o Adobe [!DNL EchoSign] para [!DNL SugarCRM] plug-in.

## Instalar este plug-in {#install-plugin}

1. Baixe o Adobe [!DNL EchoSign] para [!DNL SugarCRM]  arquivar arquivo do [Lista SugarExchange](http://www.sugarexchange.com/product_details.php?product=1123).
1. Faça logon [!DNL SugarCRM] com sua conta de administrador.
1. Ir para **[!UICONTROL Administração]** > **[!UICONTROL Carregador de módulo]**.

   ![Imagem](images/module-loader.png)

1. Para fazer upload do arquivo morto do Adobe [!DNL EchoSign] para [!DNL SugarCRM] plug-in, selecione **[!UICONTROL Procurar]**, selecione o arquivo e selecione **[!UICONTROL Carregar]**.
1. Após o upload do arquivo morto, selecione **[!UICONTROL Instalar]** para iniciar a instalação.
1. Revise os termos e condições e selecione **[!UICONTROL Aceitar]** > **[!UICONTROL Confirmar]**.
1. Se o plug-in for instalado com sucesso, a barra de progresso indicará 100% de sucesso.  Se a barra de progresso não atingir 100%, selecione **[!UICONTROL Exibir Log]** para ver o erro encontrado pelo SugarCRM.

   ![Imagem](images/display-log.png)

1. Após a instalação, vá para **[!UICONTROL Administração > Reparar]** e Selecionar **[!UICONTROL Reparo e reconstrução rápidos]**.

>[!NOTE]
>
>Se você estiver instalando o plug-in em [!DNL SugarCRM] OnDemand, registre um tíquete de suporte com [!DNL SugarCRM] para remover temporariamente as restrições do inspetor de pacotes do OnDemand para que o pacote possa ser instalado. Isso faz parte do processo padrão.

## Atualizar o plug-in {#upgrade-plugin}

Se você estiver atualizando o Adobe [!DNL EchoSign] para [!DNL SugarCRM] para uma versão mais recente, você deve instalar o plug-in sem desinstalar a versão anterior.
Após atualizar o plug-in, vá para **[!UICONTROL Administração]** > **[!UICONTROL Reparar]** e selecione **[!UICONTROL Reparo e reconstrução rápidos]**.

**Observação:** Se você desinstalar um plug-in anterior, não remova as tabelas durante a desinstalação. Caso contrário, você pode perder o [!DNL EchoSign] dados do contrato.

## Configurar o plug-in {#configure-plugin}

1. Se você já é um Adobe [!DNL EchoSign] cliente, continue na Etapa 2.

   Se não tiver um [!DNL EchoSign] conta, [inscreva-se para uma avaliação GRATUITA de 14 dias](https://sugarcrmintegration.echosign.com/public/login) e siga as etapas de registro online para ativar seu Adobe [!DNL EchoSign] conta.
1. Fazer logon em [Conta do Echo Sign](http://www.echosign.com) e siga estas etapas:
   1. Selecionar **[!UICONTROL Conta]** guia.
   1. Selecionar **[!UICONTROL API do EchoSign]** no lado inferior esquerdo.
   1. Selecionar **[!UICONTROL Ativar acesso à API]** e obtenha a chave de API na página.

   ![Imagem](images/enable-api-access.png)

1. No SugarCRM, vá para **[!UICONTROL Administração]** > **[!UICONTROL Configurações do Adobe EchoSign]** e insira a chave de API no campo identificado **[!UICONTROL Chave de API do EchoSign]**.
1. Opcionalmente, configure o plug-in com as seguintes configurações:

   1. Anexe PDF automaticamente ao criar um contrato a partir de uma Cotação: Selecione se deseja anexar automaticamente uma PDF da cotação se uma [!DNL SugarCRM] O usuário cria um contrato EchoSign a partir do módulo Cotas.
   1. Gerenciar lista de destinatários: Selecione quais módulos são exibidos no subpainel Destinatário no [!DNL EchoSign] Módulo Contratos. Isso também adiciona o [!DNL EchoSign] Subpainel Contratos a esses módulos.
   1. Adicione os botões de envio a esses módulos: Selecione se você deseja que a opção Criar [!DNL EchoSign] Botão/ação do contrato a ser incluído nas ações principais do módulo Cota.
   1. Selecionar **[!UICONTROL Salvar]** para armazenar suas configurações.

**Observação:** A Adobe [!DNL EchoSign] para [!DNL SugarCRM] plug-in requer o [Extensão SOAP do PHP](http://www.php.net/manual/en/book.soap.php). Para ativar o suporte a SOAP, configure o PHP com enable-soap.

## Obter atualizações do contrato (por [!DNL SugarCRM] versões 6.3 ou superior) {#get-agreement-updates}

Para a versão 6.3 e posterior, você pode usar as duas opções a seguir para obter atualizações do contrato. Nas versões anteriores do SugarCRM, o plug-in por padrão oferece apenas o Método de retorno de chamada (Opção 1).

### Opção 1: Configurar o método de retorno de chamada para enviar atualizações ao EchoSign

Se o seu site for voltado para o público, você poderá fazer com que o Adobe EchoSign execute ping em seu [!DNL SugarCRM] sempre que ocorrer um novo evento. [!DNL SugarCRM] em seguida, atualiza o status do contrato, os eventos e o download do documento assinado (se assinado) automaticamente e em tempo real. (Se você estiver atrás de um firewall, precisará colocar o [!DNL EchoSign] endereços IP do servidor ou use o método de tarefa agendada para atualizar os contratos do EchoSign (descrito na próxima seção deste guia).

1. Ir para **[!UICONTROL Administração]** > **[!UICONTROL Configurações do Adobe EchoSign]**.
1. Marque a caixa de seleção **[!UICONTROL Usar método de retorno de chamada do EchoSign]** para atualizar eventos e status de contratos.
1. Selecionar **[!UICONTROL Salvar]**.

### Opção 2: Configurar um Job Agendado para [!DNL SugarCRM] Instâncias atrás de um firewall

O [!DNL EchoSign] para [!DNL SugarCRM] plug-in também pode usar um Job Agendado para consultar [!DNL EchoSign] para obter atualizações de Contratos Enviados para Assinatura. O método de consulta de trabalho agendado pode ser usado se você tiver um local [!DNL SugarCRM] a instalação está atrás de um firewall.

Para configurar:

1. Ir para **[!UICONTROL Administração]** > **[!UICONTROL Agendador]**.
1. No menu suspenso da guia, selecione **[!UICONTROL Criar Agendador]**.
1. Informe um Nome de Job.
1. Para o campo Cargo, selecione **[!UICONTROL Adobe EchoSign Status Updater]**.
1. Defina o job para ser executado com a frequência necessária. Sugerimos configurá-lo para ser executado a cada 10 minutos, o que significa que, depois que um contrato é aberto, lido ou assinado, pode levar até 10 minutos para [!DNL SugarCRM] informações.

   **Observação:** Se você tiver muitos contratos enviados para assinatura, a execução muito frequente pode causar lentidão no sistema.

   ![Imagem](images/echosign-status-updater.png)

1. Ir para **[!UICONTROL Administração]** > **[!UICONTROL Configurações do Adobe EchoSign]**.
1. Desmarque a caixa **[!UICONTROL Usar método de retorno de chamada do EchoSign]** para atualizar eventos e status de contratos.
1. Selecionar **[!UICONTROL Salvar]**.
Observação: Ativar Agendadores em [!DNL SugarCRM] para que isso funcione.

Para adicionar contratos do EchoSign a outros [!DNL SugarCRM] módulos:

1. Ir para **[!UICONTROL Administração]** > **[!UICONTROL Studio]**.
1. Na árvore de pastas da coluna esquerda, selecione o módulo a ser adicionado [!DNL EchoSign] Contratos.
1. Selecionar **[!UICONTROL Relações]**> **[!UICONTROL Adicionar Relações]**.
1. No menu suspenso, selecione Tipo como **[!UICONTROL Um para muitos]** e Módulo como **[!UICONTROL Contratos do EchoSign]**.
1. Selecionar **[!UICONTROL Salvar e implantar]**.

   ![Imagem](images/save-and-deploy.png)

   [!DNL EchoSign] Os contratos agora aparecem no módulo e os contratos podem ser criados e rastreados lá.

   ![Imagem](images/echosign-agreements.png)

**Outras Etapas de Configuração**

* **Ocultando [!DNL EchoSign] Módulos**: Você pode ocultar o [!DNL EchoSign] Destinatários e [!DNL EchoSign] Módulos de eventos acessando Administração&quot; Guias e subpainéis do módulo de exibição e movendo-os para a coluna oculta.
* **Desativando o packageScan**: Se você ativou o packageScan em seu próprio sistema, será necessário desativá-lo durante a instalação. Se estiver usando [!DNL SugarCRM] Sob demanda, contato [!DNL SugarCRM] suporte para desativar o packageScan para você.

## Desinstale o plug-in {#uninstall-plugin}

1. Faça logon [!DNL SugarCRM] com sua conta de administrador.
1. Ir para **[!UICONTROL Administração]** > **[!UICONTROL Carregador de módulo]**.
1. Selecionar **[!UICONTROL Desinstalar]** ao lado do [!UICONTROL Plug-in EchoSign para SugarCRM].
1. Selecionar **[!UICONTROL Confirmar]** para iniciar a desinstalação. Você também pode optar por remover as tabelas de banco de dados criadas para o plug-in.

   ![Imagem](images/uninstall-plugin.png)

   Se o plug-in for desinstalado com sucesso, a barra de progresso indicará 100% de sucesso. Se a barra de progresso não atingir 100%, selecione [!UICONTROL Exibir Log] para ver o erro encontrado pelo SugarCRM.

   ![Imagem](images/uninstall-display-log.png)

## Usar Adobe [!DNL EchoSign] para [!DNL SugarCRM] {#use-echosign-for-sugarcrm}

Você pode criar um Adobe [!DNL EchoSign] contrato associado a uma conta, contato, cotação ou outro [!DNL SugarCRM] módulos. Você pode anexar arquivos, especificar destinatários e enviar para assinatura. Adobe [!DNL EchoSign] atualizações [!DNL SugarCRM] com o status atual do contrato e armazena o contrato assinado em [!DNL SugarCRM] quando estiver totalmente executado.

### Criar e editar um Adobe [!DNL EchoSign] contrato {#create-edit-agreements}

Você pode criar Contratos por meio do [!DNL EchoSign] Módulo Contratos ou por meio de módulos configurados por um [!DNL SugarCRM] administrador.

1. No menu [!UICONTROL Ações] na lista [!UICONTROL Contratos do EchoSign] , selecione **[!UICONTROL Criar contrato do EchoSign]**.
1. Na seção principal do [!DNL EchoSign] Contrato, insira as seguintes informações ou selecione entre várias opções de contrato:

   1. **[!UICONTROL Nome:]** Insira um nome para o contrato.
   1. **[!UICONTROL Tipo de assinatura:]** Selecione o tipo de assinatura aceito para o documento. As opções são Assinatura eletrônica e Assinatura por fax.
   1. **[!UICONTROL Também preciso assinar este contrato:]** Indique se o remetente também precisa assinar o contrato.
   1. **[!UICONTROL Ordem de assinatura:]** Se a opção anterior Eu também preciso assinar este contrato estiver marcada, selecione também a ordem na qual o remetente e os destinatários devem assinar.
   1. **[!UICONTROL Lembrar destinatários de assinar:]** Selecione a frequência com que um destinatário deve ser lembrado de assinar um documento. As opções são Diariamente ou Semanalmente.
   1. **[!UICONTROL Dias até o prazo de assinatura:]** Especifique o número de dias até a assinatura do contrato.
   1. **[!UICONTROL Exibir e posicionar assinaturas ou incluir campos de formulário:]**  Selecione essa opção para visualizar o contrato antes de enviá-lo ou arraste e solte campos de assinatura, campos iniciais ou outros campos de formulário no contrato antes de enviá-lo aos destinatários. Depois de visualizar o documento ou arrastar os campos que deseja no documento, lembre-se de selecionar o botão Enviar para enviar o contrato ao destinatário.
   1. **[!UICONTROL Hospede a assinatura do primeiro signatário:]** Indique se o remetente deseja hospedar a assinatura presencial do contrato.
      * **[!UICONTROL Mensagem:]** Inclua uma mensagem para o destinatário.
      * **[!UICONTROL Conta, oportunidade, cotação:]** Selecione ou modifique a Conta, Oportunidade ou Cota associada a este contrato.
      * **[!UICONTROL Idioma:]** Especifique o idioma em que a página de assinatura e as notificações por email são exibidas aos destinatários.

      ![Imagem](images/create-agreements.png)


1. No menu [!UICONTROL Opções de segurança] seção do [!UICONTROL Contrato do EchoSign], insira as seguintes informações:

   a) **[!UICONTROL Senha necessária para assinar:]** Indique se uma senha deve ser inserida antes que um destinatário possa assinar um documento.
b) **[!UICONTROL Senha necessária para abrir:]** Indique se uma senha deve ser inserida antes que um destinatário possa abrir uma PDF do contrato ou assinar o contrato (c) **[!UICONTROL Senha:]** Especifique a senha a ser usada para assinar ou abrir um documento.
d) **[!UICONTROL Confirmar senha:]** Confirme a senha a ser usada para assinar ou abrir um documento.

1. Na outra seção do [!DNL EchoSign] Acordo, especifique as seguintes informações:

   a) **[!UICONTROL Usuário:]** Especifique um [!DNL SugarCRM] usuário. O padrão é o usuário conectado ao sistema no momento.
b) **[!UICONTROL Equipes:]** Para alterar a atribuição principal da equipe, insira o nome da nova equipe principal. Para atribuir equipes adicionais ao registro, clique em **[!UICONTROL Selecionar]** e selecione um grupo na Lista de grupos ou selecione **[!UICONTROL Adicionar a]** para adicionar campos de grupo e inserir os nomes do grupo. Para obter mais informações, consulte &#39;Atribuição de registros a usuários e equipes&#39; no [!DNL SugarCRM] Guia do aplicativo.

1. Selecionar **[!UICONTROL Salvar]**.

### [!DNL EchoSign] exibição de detalhes do contrato {#agreement-detail-view}

Após um [!DNL EchoSign] Quando o contrato é salvo, a Exibição de detalhes do contrato inclui os seguintes subpainéis:

* **[!UICONTROL Destinatários:]** Todos os contatos listados neste subpainel recebem os documentos especificados no subpainel Documentos. Você deve adicionar um ou mais destinatários antes de enviar o contrato.
* **[!UICONTROL Documentos:]** Faça upload de um novo documento ou selecione um documento já carregado no [!DNL SugarCRM] para enviar para assinatura.
* **[!UICONTROL Eventos:]** Qualquer ação relacionada ao contrato, como quando o contrato foi enviado para assinatura, visualizado ou assinado, é listada neste subpainel.
Para editar um [!DNL EchoSign] Contrato, selecione o [!UICONTROL Editar] botão na [!UICONTROL Exibição Detalhada] do acordo.

![Imagem](images/agreement-detail-view.png)

**Observação:** Depois que um contrato é enviado para assinatura, a [!UICONTROL Editar] é removido da Exibição de detalhes para preservar o registro de eventos. No entanto, você pode ativar o botão Editar . Para isso, vá para [!UICONTROL Admin] > [!UICONTROL Configurações do Adobe EchoSign] e desmarque a opção *[!UICONTROL Depois que um contrato é enviado para assinatura, desative a capacidade de editar ou excluir]*.

### Adicionar um documento a um [!DNL EchoSign] contrato {#add-document}

[!DNL SugarCRM] os usuários podem carregar um novo documento ou selecionar um documento já carregado no [!DNL SugarCRM] usando o subpainel Documentos de um registro de Contrato do EchoSign.
Para carregar um documento, selecione **[!UICONTROL Fazer upload do documento]** no [!UICONTROL Documentos] subpainel.

Consulte a seção &quot;Módulo Documentos&quot; do [!DNL SugarCRM] Guia do aplicativo para obter mais informações sobre os campos individuais desse formulário.

Para selecionar um documento, clique em **[!UICONTROL Selecionar]** no subpainel Documentos. Consulte &quot;Exibindo e Gerenciando Informações de Registros&quot; no [!DNL SugarCRM] Application Guide para obter mais informações sobre como gerenciar informações relacionadas em subpainéis.

![Imagem](images/add-document-to-agreement.png)

### Especifique um destinatário para um [!DNL EchoSign] contrato {#specify-recipient}

1. No menu [!UICONTROL Destinatário] subpainel de um [!DNL EchoSign] Contrato, selecione **[!UICONTROL Adicionar destinatário]**.
1. Insira as seguintes informações: a) [!UICONTROL Destinatário:] Selecione o tipo de destinatário no menu suspenso. Digite o nome ou o endereço de email do destinatário no campo de texto. [!DNL SugarCRM] O pesquisa o nome à medida que você digita e oferece uma lista de seleções. Selecione um nome se uma correspondência for encontrada. Você também pode selecionar o ícone de seta para selecionar um nome em uma janela pop-up. Para apagar o nome do campo, selecione o **[!UICONTROL X]** ícone.
b) [!UICONTROL Função:] Selecione uma função no menu suspenso. As opções são Signatário, CC e Aprovador. Um aprovador não precisa assinar o documento.
1. Selecione Salvar.

![Imagem](images/add-recipient-to-agreement.png)

### Enviar contratos para assinatura {#send-for-signature}

Quando os contratos estiverem prontos para serem enviados para assinatura, selecione **[!UICONTROL Send for Signature]** no menu suspenso na parte superior esquerda da página. Em seguida, os destinatários recebem um email informando-os sobre os documentos que aguardam a assinatura. Depois que os destinatários assinam o documento, o remetente recebe uma notificação por email.
Se a [!UICONTROL Hospedar assinatura para o primeiro signatário] estiver marcada, você pode selecionar **[!UICONTROL Send for Signature]** para permitir que o signatário assine o documento com o remetente presente.

![Imagem](images/send-for-signature.png)

A **[!UICONTROL Hospedar assinatura para signatário atual]** também é exibido ao lado do [!UICONTROL Hospedar assinatura para o primeiro signatário] , que pode ser acessado até que o documento seja assinado. Você pode usar este link para hospedar a assinatura do contrato para vários signatários ou para reabrir a janela pop-up se ela tiver sido fechada acidentalmente.
Se [!UICONTROL Exibir e posicionar assinaturas ou incluir campos de formulário] estiver marcada, selecione **[!UICONTROL Send for Signature]** para permitir que o remetente visualize o documento ou arraste os campos para o documento antes de enviá-lo. Você deve selecionar **[!UICONTROL Enviar]** nessa janela para enviar o contrato ao destinatário.

Figura 5: Selecione Send for Signature para enviar um documento a um destinatário para assinatura.

### Enviar de um registro de cotação {#send-from-quote-record}

Adobe [!DNL EchoSign] tem uma integração direta com Cotações em [!DNL SugarCRM] para que o PDF da cotação seja gerado e anexado automaticamente ao registro do contrato.
Ao exibir uma Cotação, selecione **[!UICONTROL Criar contrato do EchoSign]** para gerar a cotação e anexá-la automaticamente ao contrato. O novo contrato também associa automaticamente qualquer Oportunidade, Conta ou Cota relacionada.

![Imagem](images/create-echosign-agreement.png)

Para desativar a anexação automática do PDF da cotação ao contrato, vá para **[!UICONTROL Administração]** > **[!UICONTROL Configurações do Adobe EchoSign]** e desmarque a caixa *[!UICONTROL Anexe PDF automaticamente ao criar um contrato a partir de uma cotação]*.

### Cancelar um contrato {#cancel-agreement}

Você pode cancelar um [!DNL EchoSign] Contrato após ter sido enviado para uma assinatura, se todos os destinatários ainda não tiverem assinado o documento. A [!UICONTROL Cancelar Contrato] aparece na Exibição de detalhes de um contrato depois que um documento é enviado para assinatura. Selecionar **[!UICONTROL Cancelar Contrato]** para cancelar o contrato.

![Imagem](images/cancel-agreement.png)

Observação: Se um [!DNL EchoSign] O contrato é enviado para assinatura e o registro é excluído. Você deve cancelar o contrato antes de excluí-lo.

### Monitore assinaturas {#track-signatures}

O [!UICONTROL Eventos] subpainel de um [!DNL EchoSign] O contrato acompanha o status dos contratos enviados para assinatura. Para ver as atualizações mais recentes em um [!DNL EchoSign] Contrato, selecione **[!UICONTROL Atualizar status]**. O [!UICONTROL Atualizar status] está disponível somente depois que um contrato é enviado para assinatura.

![Imagem](images/update-cancel-status.png)

Depois que um contrato é enviado para assinatura, selecione **[!UICONTROL Atualizar status]** para recuperar o status mais recente.

![Imagem](images/events-subpanel.png)

### Enviar lembretes {#send-reminders}

Para enviar um lembrete ao signatário atual após o envio do contrato, selecione **[!UICONTROL Enviar lembrete]**. Ele envia imediatamente um lembrete por email ao signatário atual sobre o contrato que está aguardando assinatura.

![Imagem](images/send-reminder.png)
