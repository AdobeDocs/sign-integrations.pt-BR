---
title: Guia de instalação do Veeva Vault
description: Guia de instalação para ativar a integração do Adobe Sign com a Veeva
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 5d61a428-06e4-413b-868a-da296532c964
source-git-commit: c6c0257204ab45776450f77a5a95291a99371063
workflow-type: tm+mt
source-wordcount: '3909'
ht-degree: 3%

---

# [!DNL Veeva Vault] Guia de instalação{#veeva-installation-guide}

[**Entre em contato com o suporte do Adobe Acrobat Sign**](https://adobe.com/go/adobesign-support-center_br)

## Visão geral {#overview}

Este documento explica como estabelecer integração do Adobe Acrobat Sign com [!DNL Veeva Vault] plataforma. [!DNL Veeva Vault] é uma plataforma de ECM (Enterprise Content Management, gerenciamento de conteúdo corporativo) desenvolvida para ciências biológicas. Um &quot;Cofre&quot; é um repositório de dados e conteúdo com uso típico para registros normativos, relatórios de pesquisa, aplicativos de concessões, contratos gerais e muito mais. Uma única empresa pode ter vários &quot;cofres&quot; que devem ser mantidos separadamente.

As etapas de alto nível para concluir a integração são:

* Ative sua conta administrativa no Adobe Acrobat Sign (somente novos clientes).
* Crie objetos para controlar o histórico do ciclo de vida de um contrato no Vault.
* Crie um novo perfil de segurança.
* Configure um grupo no Adobe Acrobat Sign para manter o [!DNL Veeva Vault] usuário de integração.
* Crie campos de documento e representações.
* Configurar ações da Web e atualizar o ciclo de vida do documento.
* Criar tipo de documento configuração de usuário e função de usuário.
* Conecte o Veeva Vault ao Adobe Acrobat Sign usando middleware.

>[!NOTE]
>
>O administrador do Adobe Sign deve executar as etapas de configuração do Adobe Acrobat Sign no Adobe Acrobat Sign.

## Configure [!DNL Veeva Vault] {#configure-veeva}

Para configurar [!DNL Veeva Vault] para integração com o Adobe Acrobat Sign, você deve implementar as etapas listadas abaixo.

### Etapa 1. Criar grupo {#create-group}

Para configurar o Adobe Acrobat Sign para [!DNL Vault], um novo grupo chamado *Adobe Sign Admin Group* é criado. Esse grupo é usado para definir a segurança de nível de campo do documento para campos relacionados ao Adobe Acrobat Sign e deve incluir *Perfil de integração do Adobe Sign* por padrão.

![Imagem dos detalhes do evento de assinatura](images/create-admin-group.png)

### Etapa 2. Implantar o pacote {#deploy-package}

[Implantar o pacote](https://helpx.adobe.com/content/dam/help/en/PKG-AdobeSign-Integration.zip) e siga as etapas. Depois de implantado, o pacote cria:

* Objetos personalizados: Objeto Signature, objeto Signatory, objeto Signature Event, objeto Process Locker
* Layout da página do objeto de assinatura
* Layout da página do objeto Evento de assinatura
* Layout de página do objeto Signatário
* Layout da página do objeto Process Locker
* Layout da página do objeto Log de Tarefas de Integração do Adobe Sign
* Tipo de representação do Adobe Sign
* Tipo de representação original
* Assinatura de campo compartilhado__c
* Ação da Web do Adobe Sign
* Cancelar ação do Adobe Sign na Web
* Conjunto de permissões das ações de administrador do Adobe Sign
* Perfil de segurança do Adobe Sign Integration Profile
* Função de aplicativo Adobe Sign Função de administrador
* Grupo de tipos de documento &quot;Documento do Adobe Sign&quot;
* Objeto de log da Tarefa de Integração do Adobe Sign

#### Objeto Signature {#signature-object}

O objeto de assinatura é criado para armazenar informações relacionadas ao contrato. Um objeto Signature é um banco de dados que contém informações nos seguintes campos específicos:

**Campos de objeto de assinatura**

| Campo | Rótulo | Tipo | Descrição |
| --- | --- | ---| --- | 
| external_id__c | ID do contrato | Sequência de caracteres (100) | Contém a ID de contrato exclusiva do Adobe Acrobat Sign |
| file_hash__c | Hash de Arquivo | Sequência de caracteres (50) | Contém a soma de verificação md5 do arquivo que foi enviado para o Adobe Acrobat Sign |
| name__v | Nome | Sequência de caracteres (128) | Mantém o nome do contrato |
| sender__c | Remetente | Objeto (Usuário) | Mantém a referência ao usuário do Vault que criou o contrato |
| signature_status__c | Status da assinatura | Sequência de caracteres (75) | Mantém o status do contrato no Adobe Acrobat Sign |
| signature_type__c | Tipo de assinatura | Sequência de caracteres (20) | Mantém o tipo de assinatura do contrato no Adobe Acrobat Sign (escrito ou ESIGN) |
| start_date__c | Data de início | DataHora | Data em que o contrato foi enviado para assinatura |
| cancellation_date__c | Data de cancelamento | DataHora | Mantém a data em que o contrato foi cancelado. |
| completed_date__c | Data de conclusão | DataHora | Mantém a data em que o contrato foi concluído. |
| viewable_rendition_used__c | Reprodução Visível Usada | Boolean | Sinalizador que indica se a representação visível foi enviada para assinatura. (por padrão, é verdadeiro) |
| plugin_version__c | Versão do plug-in | Texto (10) | É usado para permitir o processamento apropriado de todos os contratos criados antes que uma nova versão 4.0 seja implantada. Observação: Depois que a versão 4.0 do aplicativo Web personalizado for implantada, esse campo será definido como 4.0 sempre que o registro de assinatura for criado. |
| external_environment__c | Ambiente externo | Texto (20) | Mantém o nome do ambiente do Adobe Sign no qual o contrato foi criado. |

![Imagem dos detalhes do objeto de assinatura](images/signature-object-details.png)

#### Objeto signatário {#signatory-object}

O objeto Signatário é criado para armazenar informações relacionadas aos participantes em um contrato. Contém informações nos seguintes campos específicos:

**Campos de objeto do signatário**

| Campo | Rótulo | Tipo | Descrição |
| --- | --- | ---| --- | 
| email__c | Email | Sequência de caracteres (120) | Contém a ID de contrato exclusiva do Adobe Acrobat Sign |
| external_id__c | ID do participante | Sequência de caracteres (80) | Contém o identificador exclusivo do participante do Adobe Acrobat Sign |
| name__v | Nome | Sequência de caracteres (128) | Mantém o nome do participante do Adobe Acrobat Sign |
| order__c | Ordem | Número | Contém o número do pedido do participante do contrato do Adobe Acrobat Sign |
| role__c | Função | Sequência de caracteres (30) | Mantém a função do participante do contrato do Adobe Acrobat Sign |
| signature__c | Assinatura | Objeto (assinatura) | Mantém a referência ao registro pai da assinatura |
| signature_status__c | Status da assinatura | Sequência de caracteres (100) | Mantém o status do participante do contrato do Adobe Acrobat Sign |
| user__c | Usuário | Objeto (Usuário) | Mantém a referência ao registro de usuário do signatário se o participante for um usuário do Vault |

![Imagem do signatário](images/signatory-object-details.png)

#### Objeto Evento de assinatura {#signature-event}

O objeto Evento de assinatura é criado para armazenar informações relacionadas a eventos de um contrato. Contém informações nos seguintes campos específicos:

Campos de objeto do evento de assinatura

| Campo | Rótulo | Tipo | Descrição |
| --- | --- | ---| --- | 
| acting_user_email__c | Email do usuário em ação | Sequência de caracteres | Contém o email do usuário do Adobe Acrobat Sign que executou a ação que gerou o evento |
| acting_user_name__c | Nome de usuário ativo | Sequência de caracteres | Contém o nome do usuário do Adobe Acrobat Sign que executou a ação que gerou o evento |
| descrição__c | Descrição | Sequência de caracteres | Contém a descrição do evento do Adobe Acrobat Sign |
| event_date__c | Data do evento | DataHora | Mantém a data e a hora do evento do Adobe Acrobat Sign |
| event_type__c | Tipo de evento | Sequência de caracteres | Contém o tipo de evento do Adobe Acrobat Sign |
| name__v | Nome | Sequência de caracteres | Nome do evento gerado automaticamente |
| participant_comment__c | Comentário do participante | Sequência de caracteres | Mantém o comentário do participante do Adobe Acrobat Sign, se houver |
| participant_email__c | Email do participante | Sequência de caracteres | Contém o email do participante do Adobe Acrobat Sign |
| participant_role__c | Função do participante | Sequência de caracteres | Tem a função de participante do Adobe Acrobat Sign |
| signature__c | Assinatura | Objeto (assinatura) | Mantém a referência ao registro pai da assinatura |
| external_id__c | ID Externa | Texto (200) | Identificador de Evento do Contrato de Retenção gerado pelo Adobe Sign. |

![Imagem](images/signature-event-object-details.png)

#### Objeto Process Locker {#process-locker}

Um objeto Process Locker é criado para bloquear o processo de integração do Adobe Acrobat Sign. Não requer campos personalizados.

![Imagem dos detalhes do evento de assinatura](images/process-locker-details.png)

#### Objeto de Log da Tarefa de Integração do Adobe Sign {#task-log}

Criar Log de Tarefas de Integração do Adobe Sign (as_int_task_log__c). É um objeto de alto volume usado para rastrear a execução de AgreementsEventsSynchronizerJob e AgreementsEventsProcessingJob.
AgreementsEventsSynchronizerJob: Esta tarefa garante que todos os Eventos de contrato ausentes do Adobe Sign sejam criados como Eventos de assinatura ativos no Vault para todas as assinaturas criadas no Vault nos últimos N dias.
AgreementsEventsProcessingJob: Esta tarefa garante que todos os Documentos com registros de Evento de assinatura ativos sejam processados dependendo do tipo de evento.

Campos de Objeto de Log de Tarefas de Integração do Adobe Sign

| Campo | Rótulo | Tipo | Descrição |
|:--|:--|:--|:---------| 
| start_date__c | Data de início | DataHora | Data de início da tarefa |
| end_date__c | Data de término | DataHora | Data de Término da Tarefa |
| task_status__c | Status da Tarefa | Lista de seleção | Armazena o status da tarefa: <br><br> Concluído (task_completed__c) <br><br> Concluído com Erros (task_completed_with_errors__c) <br><br> Falha (task_failed__c) |
| task_type__c | Tipo de Tarefa | Lista de seleção | Tipo de tarefa de retenção: <br><br> Sincronização de eventos dos contratos (agreements_events_synchronization__c) <br><br> Processamento de Eventos de Acordos (agreements_events_processing__c) |
| messages__c | Mensagem | Longo (32000) | Retém a mensagem da tarefa |

![Imagem dos detalhes do objeto do log de tarefas](images/task-log.png)

![Imagem de campos de objeto do log de tarefas](images/task-log-fields.png)

Os objetos Signature, Signatory, Signature Event, Process Locker e Task Log que fazem parte do pacote de implantação têm a propriedade &quot;Audit data changes for this object&quot; ativada por padrão.

**Observação:** Você pode fazer com que o Vault capture as alterações de dados do registro do objeto nos registros de auditoria ativando a configuração Auditar alterações de dados. Essa configuração fica desativada por padrão. Depois de ativar essa configuração e criar registros, você não poderá mais desativá-la. Se essa configuração estiver desativada e houver registros, somente um Proprietário do Vault poderá atualizá-la.

#### **Exibir participantes e histórico do objeto de assinatura** {#display-participants-history}

O objeto Signature que faz parte do pacote de implantação vem com o [Layout da página de detalhes da assinatura](https://vvtechpartner-adobe-rim.veevavault.com/ui/#admin/content_setup/object_schema/pagelayout?t=signature__c&amp;d=signature_detail_page_layout__c). O Layout de página tem seções para Participantes e Histórico.

* O *Participantes* A seção Objetos Relacionados está configurada conforme mostrado na imagem abaixo.

   ![Imagem](images/edit-related-objects.png)

* Você pode editar as colunas a serem exibidas para os Participantes, conforme mostrado abaixo.

   ![Imagem](images/set-columns-to-display.png)

* O *Histórico* A seção Objetos Relacionados está configurada conforme mostrado na imagem abaixo.

   ![Imagem](images/edit-related-object-in-history.png)

* Você pode editar as colunas a serem exibidas no Histórico, conforme mostrado abaixo.

   ![Imagem](images/select-columns-to-display.png)

#### **Exibir participantes e histórico de auditoria do documento do Adobe Acrobat Sign** {#view-participants-audit-history}

* Para exibir os Participantes e o histórico de auditoria do documento do Adobe Acrobat Sign, selecione o link na seção &#39;Adobe Signature&#39; do documento.

   ![Imagem](images/view-participants-audit-history.png)

* A página que é aberta exibe os Participantes e o Histórico do documento do Adobe Acrobat Sign, conforme mostrado abaixo.

   ![Imagem](images/participants-and-history.png)

* Veja a trilha de auditoria para assinatura conforme mostrado abaixo.

   ![Imagem](images/audit-trail.png)

### Etapa 3. Configurar perfis de segurança {#security-profiles}

A implantação de pacote bem-sucedida na Etapa 2 cria o perfil de integração do Adobe Sign. O Perfil de integração do Adobe Sign é atribuído à conta do sistema e é usado pela integração ao chamar as APIs do Vault. Este perfil permite permissões para:

* APIs do Vault
* Lendo, criando, editando e excluindo: Assinatura, Assinatura, Eventos de assinatura e objetos do Process Locker

Você deve atualizar o Adobe Sign Admin Group (criado na Etapa 1) definindo o perfil de segurança incluído como Perfil de integração do Adobe Sign, conforme mostrado na imagem abaixo.

![Imagem dos detalhes do evento de assinatura](images/security-profiles.png)

### Etapa 4. Criar usuário {#create-user}

O usuário da conta de sistema do Vault da integração do Adobe Acrobat Sign deve:

* Ter um perfil de integração do Adobe Sign
* Tem um perfil de segurança
* Tem uma política de segurança específica que desativa a expiração da senha
* Seja membro do Adobe Sign Admin Group.

Para isso, siga as etapas abaixo:

1. Crie uma conta do sistema do Vault que seja usuário da integração do Adobe Acrobat Sign.

   ![Imagem dos detalhes do evento de assinatura](images/create-user.png)

2. Adicione o usuário ao Adobe Sign Admin Group.

   ![Imagem dos detalhes do evento de assinatura](images/add-user.png)

### Etapa 5. Configurar Grupo de Tipos de Documento {#create-document-type-group}

Quando você implanta o pacote do Adobe Acrobat Sign, ele cria um registro de Grupo de tipos de documento chamado &quot;Documento do Adobe Sign&quot;.

![Imagem de grupos de tipos de documento](images/document-type-groups.png)

Você deve adicionar esse grupo de tipos de documento para todas as classificações de documento qualificadas para o processo do Adobe Acrobat Sign. Como a propriedade de grupo de tipo de documento não é herdada do tipo para o subtipo nem do subtipo para o nível de classificação, ela deve ser definida para cada classificação de documento elegível para o Adobe Acrobat Sign.

![Imagem dos detalhes de edição do documento](images/document-edit-details.png)

**Observação:** Se o objeto Configuração da função do usuário não contiver o campo que se refere ao objeto Grupo de tipos de documento, você deverá adicionar o campo. Para isso, vá para **[!UICONTROL Objeto]** > **[!UICONTROL Configuração de Função de Usuário]** > **[!UICONTROL Campos]** e conclua as etapas necessárias, conforme mostrado na imagem abaixo.

![Imagem da configuração da função de usuário](images/create-setup-field.png)

![Imagem do tipo de documento](images/document-type.png)

### Etapa 6. Criar Configuração de Função de Usuário {#create-user-role-setup}

Depois que os ciclos de vida são configurados corretamente, o sistema deve garantir que o usuário administrador do Adobe Sign seja adicionado pelo DAC para todos os documentos qualificados para o processo do Adobe Acrobat Sign. Isso é feito criando o registro apropriado de Configuração de função de usuário que especifica:

* Tipo de documento Grupo como documento do Adobe Sign
* Função do aplicativo como função de administrador do Adobe Sign
* Usuário de integração

![Imagem da configuração da função de usuário](images/user-role-setup.png)

### Etapa 7. Configurar Campos de Documento {#create-fields}

A implantação do pacote cria o seguinte novo campo de documento compartilhado que é necessário para estabelecer a integração:

* Assinatura (signature__c)

![Imagem](images/document-fields.png)

Para configurar Campos de documento:

1. Vá para a guia Configuração e selecione **[!UICONTROL Campos de documento]** > **[!UICONTROL Campos compartilhados]**.
1. No campo Seção de Exibição, selecione **[!UICONTROL Criar Seção de Exibição]** e atribuir **[!UICONTROL Assinatura Adobe]** como o rótulo Seção.

   ![Imagem](images/create-display-section.png)

1. Para os Campos de documento compartilhados (assinatura__c), atualize a seção da interface do usuário com **[!UICONTROL Assinatura Adobe]** como o rótulo da seção.
1. Adicione os dois campos compartilhados a todos os tipos de documento qualificados para assinatura do Adobe Acrobat. Para fazer isso, na página Documento base, selecione **[!UICONTROL Adicionar]** > **[!UICONTROL Campo compartilhado existente]** no canto superior direito.

   ![Imagem](images/create-document-fields.png)

   ![Imagem](images/add-existing-fields.png)

   ![Imagem](images/use-shared-fields.png)

1. Ambos os campos devem ter uma segurança específica que permita que apenas membros do Adobe Sign Admin Group atualizem seus valores.

   ![Imagem](images/security-overrides.png)

Desativar Sobreposições do Vault (disable_vault_overlay__v) é um campo compartilhado existente. Opcionalmente, o campo pode ter uma segurança específica que permite que apenas membros do grupo de administradores do Adobe Sign atualizem seu valor.

### Etapa 8. Declarar representações de documento {#declare-renditions}

O novo tipo de representação chamado *Adobe Sign Rendition (adobe_sign_rendition__c)* é usado pela integração do Vault para carregar documentos PDF assinados no Adobe Acrobat Sign. Você deve declarar a representação Adobe Sign para cada tipo de documento qualificado para a Assinatura do Adobe Acrobat.

![Imagem de tipos de representação](images/rendition-type.png)

![Imagem](images/edit-details-clinical.png)

O novo tipo de representação chamado *Representação original (original_rendition__c)* é usado pela integração do Vault como o nome da representação que deve ser usada para armazenar a representação visível original se o documento assinado for importado como representação visível.

![Imagem](images/original-rendition.png)

### Etapa 9. Atualizar ações da Web {#web-actions}

A integração do Adobe Acrobat Sign com o Vault exige que você crie e configure as duas ações da Web a seguir:

* **Criar Adobe Sign**: Ele cria ou exibe o Contrato do Adobe Acrobat Sign.

   Tipo: Destino do documento: Exibir dentro das Credenciais do Vault: Habilitar credenciais de Post Session via URL de Post Message: <https://api.na1.adobesign.com/api/gateway/veevavaultintsvc/partner/agreement?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&vaultid=${Vault.id}&useWaitPage=true>

   ![Image of create Adobe Sign](images/create-adobe-sign.png)

* **Cancelar Adobe Sign**: Ele cancela um contrato existente no Adobe Acrobat Sign e reverte o estado de um documento para o estado inicial.

   Tipo: Destino do documento: Exibir dentro das Credenciais do Vault: Habilitar credenciais de Post Session via URL de Post Message: : <https://api.na1.adobesign.com/api/gateway/veevavaultintsvc/partner/agreement/cancel?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&vaultid=${Vault.id}&useWaitPage=true>

   ![Image of cancel Adobe Sign](images/cancel-adobe-sign.png)

### Etapa 10. Atualizar ciclo de vida do documento {#document-lifecycle}

Para cada tipo de documento qualificado para a Assinatura Adobe, você deve atualizar o ciclo de vida do documento correspondente adicionando novos estados e funções do ciclo de vida.

O ciclo de vida do contrato do Adobe Acrobat Sign tem os seguintes estados:

* RASCUNHO
* AUTHORING ou DOCUMENTS_NOT_YET_PROCESSED
* OUT_FOR_SIGNATURE ou OUT_FOR_APPROVAL
* ASSINADO ou APROVADO
* CANCELADO
* EXPIRADO

Para atualizar o ciclo de vida do documento, siga as etapas abaixo:

1. Adicionar função de Ciclo de Vida. A função de aplicativo Administrador do Adobe Sign deve ser adicionada em todos os ciclos de vida usados por documentos qualificados para assinatura do Adobe Acrobat, conforme mostrado abaixo.

   ![Imagem das funções de administrador do ciclo de vida](images/document-lifecycle-admin-role.png)

   A função de administrador deve ser criada com as seguintes opções:

   * Habilitado o Controle de Acesso Dinâmico.
   * Regras de compartilhamento de documentos que incluem apenas Grupo de tipos de documentos, conforme mostrado na imagem abaixo.

   ![Imagem da regra de compartilhamento do Adobe Sign](images/adobe-sign-sharing-rule.png)

2. Crie estados do ciclo de vida. Para isso, vá para **[!UICONTROL Configurações]** > **[!UICONTROL Configuração]** > **[!UICONTROL Ciclos de vida do documento]** > **[!UICONTROL Ciclos de vida gerais]** > **[!UICONTROL Estados]** > **[!UICONTROL Criar]**. Em seguida, crie os seguintes estados:

   * No Adobe Sign Draft

   ![Imagem da regra de compartilhamento do Adobe Sign](images/create-draft-state.png)

   * Na criação do Adobe Sign

   ![Imagem da regra de compartilhamento do Adobe Sign](images/create-authoring-state.png)

   * Assinatura no Adobe

   ![Imagem da regra de compartilhamento do Adobe Sign](images/create-signing-state.png)

3. Adicione ações do usuário aos estados listados abaixo.

   Quando um documento do Vault é enviado para o Adobe Acrobat Sign, seu estado deve corresponder ao estado em que o contrato está. Para fazer isso, adicione os seguintes estados em cada ciclo de vida usado por documentos qualificados para assinatura Adobe:

   * **Antes da assinatura do Adobe** (Revisado): Este é um nome de espaço reservado para o estado a partir do qual o documento pode ser enviado ao Adobe Acrobat Sign. Com base no tipo de documento, ele pode ser Estado de rascunho ou Revisado. O rótulo de estado do documento pode ser personalizado de acordo com os requisitos do cliente. Antes da assinatura do Adobe, o estado deve definir as duas seguintes ações do usuário:

      * Ação que altera o estado do documento para *No Adobe Sign Draft* estado. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento de qualquer ciclo de vida.
      * Ação que chama a Ação da Web &quot;Adobe Sign&quot;. Esse estado deve ter segurança que permita que a função de administrador do Adobe Sign: exibir documento, exibir conteúdo, editar campos, editar relacionamentos, baixar origem, gerenciar representação visível e alterar estado.

      ![Imagem do estado do ciclo de vida 1](images/lifecycle-state1.png)

      * Modificar *Revisado* Estado de Segurança Atômica, definindo *No Adobe Sign Draft* por padrão, oculto e executar somente para *Função de administrador do Adobe Sign*.
      **Observação:** Se *Função de administrador do Adobe Sign* a função não faz parte de *Segurança Atômica:Ações do Usuário*, Adicionar **[!UICONTROL Função de administrador do Adobe Sign]** selecionando **[!UICONTROL Editar]**> **[!UICONTROL Substituição de função]**. Em seguida, adicione **Função de administrador do Adobe Sign** para *Revisado* Estado.

      ![Imagem](images/lifecycle-state-reviewed.png)
      ![Imagem](images/lifecycle-state-reviewed-1.png)
      ![Imagem](images/lifecycle-state-reviewed-2.png)

   * **No Adobe Sign Draft**: Este é um nome de espaço reservado para o estado que indica que o documento já foi carregado no Adobe Acrobat Sign e que seu contrato está em um estado RASCUNHO. É um estado obrigatório. Esse estado deve definir as cinco ações do usuário a seguir:

      * Ação que altera o estado do documento para *Na criação do Adobe Sign* estado. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento de qualquer ciclo de vida.
      * Ação que altera o estado do documento para *No estado de assinatura Adobe*. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento de qualquer ciclo de vida.
      * Ação que altera o estado do documento para *Adobe Sign Cancelado* estado. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento de qualquer ciclo de vida.
      * Ação que chama a Ação da Web *Adobe Sign*.
      * Ação que chama a Ação da Web *Cancelar Adobe Sign*. Esse estado deve ter segurança que permita que a função Administrador do Adobe Sign: exibir documento, exibir conteúdo, editar campos, editar relacionamentos, baixar origem, gerenciar representação visível e alterar estado.

      ![Imagem do estado do ciclo de vida 2](images/lifecycle-state2.png)

      * Modificar *No Adobe Sign Draft* segurança atômica do estado: ações *Adobe Sign Cancelado*, *Na criação do Adobe Sign*, *Assinatura no Adobe* deve estar oculto para todos, exceto para a função de administrador do Adobe Sign
      **Observação:** Se *Função de administrador do Adobe Sign* não faz parte de *Segurança atômica: Ações do usuário*, adicionar **[!UICONTROL Função de administrador do Adobe Sign]** selecionando **[!UICONTROL Editar]** > **[!UICONTROL Substituição de função]**. Em seguida, adicione **[!UICONTROL Função de administrador do Adobe Sign]** função para *No Adobe Sign Draft* Estado.

      ![Imagem](images/atomic-security.png)

   * **Na criação do Adobe Sign**: É um nome de espaço reservado para o estado que indica que o documento já foi carregado no Adobe Acrobat Sign e que seu contrato está no estado AUTHORING ou DOCUMENTS_NOT_YET_PROCESSED. É um estado obrigatório. Esse estado deve ter quatro ações de usuário definidas:

      * Ação que altera o estado do documento para o estado Cancelado do Adobe Sign. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento, independentemente do ciclo de vida.
      * Ação que altera o estado do documento para No estado de assinatura do Adobe. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento, independentemente do ciclo de vida.
      * Ação que chama a Ação da Web &quot;Adobe Sign&quot;
      * Ação que chama a Ação da Web &quot;Cancelar Adobe Sign&quot;. Esse estado deve ter segurança que permita que a função Administrador do Adobe Sign: exibir documento, exibir conteúdo, editar campos, editar relacionamentos, baixar origem, gerenciar representação visível e alterar estado.

      ![Imagem do estado do ciclo de vida 3](images/lifecycle-state3.png)

      * Modificar *Na criação do Adobe Sign* segurança atômica do estado: ações *Adobe Sign Cancelado* e *Assinatura no Adobe* deve estar oculto para todos, exceto para a função de administrador do Adobe Sign
      **Observação:** Se *Função de administrador do Adobe Sign* não faz parte de *Segurança atômica: Ações do usuário*, adicionar **[!UICONTROL Função de administrador do Adobe Sign]** selecionando **[!UICONTROL Editar]** > **[!UICONTROL Substituição de função]**. Em seguida, adicione **[!UICONTROL Função de administrador do Adobe Sign]** função para *Na criação do Adobe Sign* Estado.

      ![Imagem](images/adobe-sing-authoring.png)

   * **Assinatura no Adobe**: É um nome de espaço reservado para o estado que indica que o documento foi carregado no Adobe Acrobat Sign e que seu contrato já foi enviado aos participantes (estado OUT_FOR_SIGNATURE ou OUT_FOR_APPROVAL). É um estado obrigatório. Esse estado deve ter as seguintes cinco ações de usuário definidas:

      * Ação que altera o estado do documento para o estado Cancelado do Adobe Sign. O estado de destino dessa ação pode ser qualquer requisito do cliente e pode ser diferente para diferentes tipos. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento, independentemente do ciclo de vida.
      * Ação que altera o estado do documento para o estado Adobe Sign Rejeitado. O estado de destino dessa ação pode ser qualquer requisito do cliente e pode ser diferente para diferentes tipos. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento, independentemente do ciclo de vida.
      * Ação que altera o estado do documento para Adobe Assinado. O estado de destino dessa ação pode ser qualquer requisito do cliente e pode ser diferente para diferentes tipos. No entanto, o nome dessa ação do usuário deve ser o mesmo para todos os tipos de documento, independentemente do ciclo de vida.
      * Ação que chama a Ação da Web *Adobe Sign*.
      * Ação que chama a Ação da Web *Cancelar Adobe Sign*. Esse estado deve ter segurança que permita que a função Administrador do Adobe Sign: exibir documento, exibir conteúdo, editar campos, editar relacionamentos, baixar origem, gerenciar representação visível e alterar estado.

      ![Imagem do estado do ciclo de vida 4](images/lifecycle-state4.png)

      * Modificar *Assinatura no Adobe* segurança atômica do estado: ações *Adobe Sign Cancelado*, *Adobe Sign rejeitado* e *Adobe assinado* deve estar oculto para todos, exceto para a função de administrador do Adobe Sign
      **Observação:** Se *Função de administrador do Adobe Sign* não faz parte de *Segurança atômica: Ações do usuário*, adicionar **[!UICONTROL Função de administrador do Adobe Sign]** selecionando **[!UICONTROL Editar]** > **[!UICONTROL Substituição de função]**. Em seguida, adicione **[!UICONTROL Função de administrador do Adobe Sign]** função para *Assinatura no Adobe* Estado.

      ![Imagem](images/in-adobe-signing-2.png)

      * **Adobe Assinado (Aprovado)**: Este é um nome de espaço reservado para o estado que indica que o documento foi carregado no Adobe Acrobat Sign e que seu contrato foi concluído (estado SIGNED ou APPROVED). É um estado obrigatório e pode ser um estado do ciclo de vida existente, como Aprovado.
Esse estado não requer ações do usuário. Ele deve ter uma segurança que permita que a função Administrador do Adobe Sign: exibir documentos, exibir conteúdo e editar campos.

   O diagrama a seguir ilustra os mapeamentos entre o contrato do Adobe Acrobat Sign e os estados do documento do Vault, em que o estado &quot;Antes da assinatura do Adobe&quot; é Rascunho.

   ![Imagem](images/sign-vault-mappings.png)

### Etapa 11. Adicionar estágio do Adobe Sign ao Ciclo de vida geral em grupos do Estágio do Ciclo de Vida

![Imagem](images/add-adobe-sign-stage.png)

### Etapa 12. Definir permissões para Função de Usuário no estado do Ciclo de Vida

Você deve definir as permissões apropriadas para cada Função de Usuário no Estado do Ciclo de Vida, conforme mostrado na imagem abaixo.

![Imagem](images/set-user-role-permissions.png)

### Etapa 13. Configurar a segurança atômica com base no estado do documento e na função de usuário

![Imagem](images/set-atomic-security.png)

### Etapa 14. Criar mensagens de documento para Adobe Sign Cancelar

![Imagem](images/create-cancel-message.png)

## Conectar [!DNL Veeva Vault] para o Adobe Acrobat Sign usando middleware {#connect-middleware}

Depois de concluir a configuração para [!DNL Veeva Vault] e a conta de administrador do Adobe Acrobat Sign, o administrador deve criar uma conexão entre as duas contas usando o middleware. O [!DNL Veeva Vault] e a conexão de conta da Adobe Acrobat Sign é iniciada pela Adobe Acrobat Sign Identity e, em seguida, é usada para armazenar o[!DNL Veeva Vault] identidade.
Para segurança e estabilidade do sistema, o administrador deve usar um [!DNL Veeva Vault] conta de sistema/serviço/utilitário, como `adobe.for.veeva@xyz.com`, em vez de uma conta de usuário pessoal, como `bob.smith@xyz.com`.

Um administrador de conta da Adobe Acrobat Sign deve seguir as etapas abaixo para se conectar [!DNL Veeva Vault] para o Adobe Acrobat Sign usando middleware:

1. Vá para a [Adobe Acrobat Sign para [!DNL Veeva Vault] Página inicial](https://static.adobesigncdn.com/veevavaultintsvc/index.html).
1. Selecionar **[!UICONTROL Login]** no canto superior direito.

   ![Imagem de logon de middleware](images/middleware_login.png)

1. Na página de logon do Adobe Acrobat Sign que é aberta, forneça o email e a senha do administrador da conta e selecione **[!UICONTROL Fazer logon]**.

   ![Imagem](images/middleware-signin.png)

   Após o logon bem-sucedido, a página exibe a ID de e-mail associada e uma guia Configurações, conforme mostrado abaixo.

   ![Imagem](images/middleware_settings.png)

1. Selecione o **[!UICONTROL Configurações]** guia.

   A página Configurações exibe as conexões disponíveis e mostra *Nenhuma conexão disponível* no caso da primeira configuração de conexão, conforme mostrado abaixo.

   ![Imagem](images/middleware_newconnection.png)

1. Selecionar **[!UICONTROL Adicionar conexão]** para adicionar uma nova conexão.

1. Na caixa de diálogo Adicionar conexão que é aberta, forneça os detalhes necessários, incluindo o [!DNL Veeva Vault] credenciais.

   As credenciais do Adobe Acrobat Sign são preenchidas automaticamente a partir do logon inicial do Adobe Sign.

   ![Imagem](images/middleware_addconnection.png)

1. Selecionar **[!UICONTROL Validar]** para validar os detalhes da conta.

   Após a validação bem-sucedida, você verá uma notificação &quot;Usuário validado com êxito&quot;, conforme mostrado abaixo.

   ![Imagem](images/middleware_validated.png)

1. Para restringir o uso a um grupo específico do Adobe Acrobat Sign, expanda a **[!UICONTROL Grupo]** e selecione um dos grupos disponíveis.

   ![Imagem](images/middleware_group.png)

1. Para anexar o relatório de auditoria à representação assinada, marque a caixa de seleção **[!UICONTROL Anexar relatório de auditoria à representação assinada]**.

   ![Imagem](images/add-audit-report.png)

1. Para permitir o provisionamento automático de usuários no Adobe Acrobat Sign, marque a caixa de seleção **[!UICONTROL Provisionamento automático de usuários do Sign]**.

   **Observação:** O Provisionamento automático de novos usuários do Adobe Acrobat Sign funciona somente se tiver sido ativado no nível de conta do Adobe Acrobat Sign no Adobe Acrobat Sign, além de ativar **[!UICONTROL Provisionamento automático de usuários do Sign]** para[!DNL Veeva Vault] Integração do Adobe Acrobat Sign conforme mostrado abaixo pelo administrador de conta do Adobe Acrobat Sign.

   ![Imagem](images/allow-auto-provisioning.png)

1. Para configurar a Representação Adobe Sign para ser exibida na Veeva em vez da Representação original, marque a caixa de seleção **[!UICONTROL Exibir representação do Acrobat Sign]**.

   ![Imagem](images/edit-connection-dispplay-adobe-sign-rendition.png)

1. Selecionar **[!UICONTROL Salvar]** para salvar a nova conexão.

   A nova conexão é exibida na guia Configurações, mostrando uma integração bem-sucedida entre [!DNL Veeva Vault] e Adobe Acrobat Sign.

   ![Imagem](images/middleware_setup.png)

