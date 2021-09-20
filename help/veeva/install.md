---
title: '[!DNL Veeva Vault] Manual de instalação'
description: Guia de instalação para habilitar a integração da Adobe Sign com a Veeva
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 5d61a428-06e4-413b-868a-da296532c964
source-git-commit: d8b7271cae9bcbe8b66311eba0317b8937ea855c
workflow-type: tm+mt
source-wordcount: '2839'
ht-degree: 2%

---

# [!DNL Veeva Vault] Manual de instalação{#veeva-installation-guide}

[**Entrar em contato com o Suporte do Adobe Sign**](https://adobe.com/go/adobesign-support-center_br)

## Visão geral {#overview}

Este documento explica como estabelecer a integração do Adobe Sign com a plataforma [!DNL Veeva Vault]. [!DNL Veeva Vault] é uma plataforma de ECM (Enterprise Content Management, gerenciamento de conteúdo corporativo) criada para ciências biológicas. Um &quot;Vault&quot; é um repositório de conteúdo e dados com uso típico para arquivos regulatórios, relatórios de pesquisa, concessões de aplicativos, contratos gerais e muito mais. Uma única empresa pode ter vários &quot;cofres&quot; que precisam ser mantidos separadamente.

As etapas de alto nível para concluir a integração são:

* Ativar sua conta administrativa no Adobe Sign (Somente novos clientes)
* Crie objetos para controlar o histórico de uma licença de contrato no Vault.
* Crie um novo perfil de Segurança.
* Configure um Grupo no Adobe Sign para manter o usuário de integração [!DNL Veeva Vault].
* Crie campos de documento e representações.
* Configure ações da Web e atualize o ciclo de vida do documento.
* Criar configuração de usuário e função de usuário do tipo de documento.

## Configure [!DNL Veeva Vault]

Para configurar [!DNL Veeva Vault] para integração com o Adobe Sign, criamos determinados objetos que ajudam a controlar o histórico de um ciclo de vida do contrato no Vault. Os administradores precisam criar os seguintes objetos:

* Assinatura
* Signatário
* Evento de assinatura
* Bloqueador de processo

### Criar objeto de assinatura  {#create-signature-object}

O objeto de assinatura é criado para armazenar informações relacionadas ao contrato. Um objeto de assinatura é um banco de dados que contém informações nos seguintes campos específicos:

**Campos de objeto de assinatura**

| Campo | Rótulo | Digitar | Descrição |
| --- | --- | ---| --- | 
| external_id__c | ID do contrato | Sequência de caracteres (100) | Contém a ID exclusiva do contrato da Adobe Sign |
| file_hash__c | Hash de arquivo | Sequência de caracteres (50) | Mantém a soma de verificação md5 do arquivo que foi enviado para o Adobe Sign |
| name__v | Nome | Sequência de caracteres (128) | Contém o nome do contrato |
| sender__c | Remetente | Objeto (Usuário) | Contém a referência ao usuário do Cofre que criou o contrato |
| signature_status__c | Status da assinatura | Sequência de caracteres (75) | Mantém o status do contrato no Adobe Sign |
| signature_type__c | Tipo de assinatura | Sequência de caracteres (20) | Possui o tipo de assinatura do contrato no Adobe Sign (ESCRITA ou ESIGN) |
| start_date__c | Data de início | DataHora | Data em que o contrato foi enviado para assinatura |
| cancelation_date__c | Data de cancelamento | DataHora | Mantém a data em que o contrato foi cancelado. |
| complete_date__c | Data de conclusão | DataHora | Mantém a data em que o contrato foi concluído. |
| viewable_rendition_used__c | Renderização visualizável usada | Boolean | Sinalizador que indica se a representação visível foi enviada para assinatura. (por padrão, é verdadeiro) |

![Imagem dos detalhes do objeto de assinatura](images/signature-object-details.png)

### Criar objeto de sinalização {#create-signatory-object}

O objeto de assinatura é criado para armazenar informações relacionadas aos participantes em um contrato. Contém informações nos seguintes campos específicos:

**Campos de objeto de sinalização**

| Campo | Rótulo | Digitar | Descrição |
| --- | --- | ---| --- | 
| email__c | Email | Sequência de caracteres (120) | Contém a ID exclusiva do contrato da Adobe Sign |
| external_id__c | ID do participante | Sequência de caracteres (80) | Contém o identificador exclusivo do participante da Adobe Sign |
| name__v | Nome | Sequência de caracteres (128) | Contém o nome do participante da Adobe Sign |
| order__c | Ordem | Número | Possui o número do pedido do participante do contrato da Adobe Sign |
| role__c | Função | Sequência de caracteres (30) | Mantém a função do participante do contrato da Adobe Sign |
| signature__c | Assinatura | Objeto (assinatura) | Mantém a referência ao registro principal da assinatura |
| signature_status__c | Status da assinatura | Sequência de caracteres (100) | Mantém o status do participante do contrato da Adobe Sign |
| user__c | Usuário | Objeto (Usuário) | Mantém a referência ao registro de usuário do signatário se o participante for um usuário do Cofre |

![Imagem dos dados do signatário](images/signatory-object-details.png)

### Criar objeto de evento de assinatura  {#create-signature-event}

O objeto Evento de assinatura é criado para armazenar informações relacionadas ao evento de um contrato. Contém informações nos seguintes campos específicos:

| Campo | Rótulo | Digitar | Descrição |
| --- | --- | ---| --- | 
| act_user_email__c | Email do usuário em ação | Sequência de caracteres | Contém o email do usuário do Adobe Sign que executou a ação que fez com que o evento fosse gerado |
| act_user_name__c | Nome de usuário em ação | Sequência de caracteres | Contém o nome do usuário do Adobe Sign que executou a ação que fez com que o evento fosse gerado |
| description__c | Descrição | Sequência de caracteres | Contém a descrição do evento Adobe Sign |
| event_date__c | Data do evento | DataHora | Mantém a data e a hora do evento da Adobe Sign |
| event_type__c | Tipo de evento | Sequência de caracteres | Mantém o tipo do evento Adobe Sign |
| name__v | Nome | Sequência de caracteres | Nome do evento gerado automaticamente |
| participante_comment__c | Comentário do participante | Sequência de caracteres | Contém o comentário do participante da Adobe Sign, se houver |
| participante_email__c | Email do participante | Sequência de caracteres | Contém o email do participante da Adobe Sign |
| participante_role__c | Função do participante | Sequência de caracteres | Mantém a função do participante da Adobe Sign |
| signature__c | Assinatura | Objeto (assinatura) | Mantém a referência ao registro principal da assinatura |

![Imagem dos detalhes do evento de assinatura](images/signature-event-object-details.png)

### Criar objeto de Bloqueio de Processo  {#create-process-locker}

Um objeto do Process Locker é criado para bloquear o processo de integração do Adobe Sign. Não requer campos personalizados.

![Imagem dos detalhes do evento de assinatura](images/process-locker-details.png)

## Criar perfis de segurança{#security-profiles}

Para uma integração bem-sucedida do Cofre, um novo perfil de segurança chamado *Perfil de Integração da Adobe Sign* é criado e a sua permissão é definida para *Ações de Administração da Adobe Sign*. O Perfil de integração da Adobe Sign é atribuído à conta do sistema e é usado pela integração ao chamar APIs do Vault. Este perfil permite permissões para:

* APIs do Vault
* Leitura, criação, edição e exclusão: Objetos de assinatura, assinatura, eventos de assinatura e bloqueio de processo

![Imagem dos detalhes do evento de assinatura](images/security-profiles.png)

Todos os perfis de segurança dos usuários que exigem acesso ao histórico da Adobe Sign no Vault devem ter permissão de leitura para os objetos de Assinatura, Assinatura e Evento de assinatura.

![Imagem dos detalhes do evento de assinatura](images/set-permissions.png)

## Criar grupo {#create-group}

Para configurar o Adobe Sign para [!DNL Vault], um novo grupo chamado *Adobe Sign Admin Group* é criado. Esse grupo é usado para definir a segurança do nível do campo do documento para campos relacionados à Adobe Sign e deve incluir *Perfil de integração da Adobe Sign* por padrão.

![Imagem dos detalhes do evento de assinatura](images/create-admin-group.png)

## Criar usuário {#create-user}

O usuário da conta de sistema do Vault da integração da Adobe Sign deve:

* Ter o perfil de integração da Adobe Sign
* Ter um perfil de segurança
* Tem uma política de segurança específica que desativa a expiração da senha
* Seja membro do Adobe Sign Admin Group.

Para garantir que o usuário da conta do sistema pertença ao Adobe Sign Admin Group para o ciclo de vida do documento específico, você precisa criar registros de Configuração da função do usuário.

## Criar Funções de Aplicativo {#create-application-roles}

Você precisa criar a função de aplicativo chamada *Função de Administrador do Adobe Sign*. Essa função deve ser definida no ciclo de vida de cada tipo de documento elegível para assinatura de Adobe. Para cada um dos estados de ciclo de vida específicos da Adobe Sign, a função de administrador da Adobe Sign é adicionada e configurada com as permissões apropriadas.

![Imagem de criar funções de aplicativo](images/create-application-roles.png)

## Criar campos de documento {#create-fields}

Para estabelecer a integração com o Adobe Sign, os administradores precisam criar os dois novos campos de documento compartilhados a seguir:

* Assinatura (signature__c)
* Permitir ações do usuário Adobe Sign (allow_adobe_sign_user_actions__c)

![Imagem dos detalhes do documento](images/create-document-fields.png)

Esses campos compartilhados devem ser adicionados a todos os tipos de documento qualificados para a Assinatura de Adobe. Ambos os campos devem ter uma segurança específica que permite que apenas os membros do Adobe Sign Admin Group atualizem seus valores.

![Imagem dos detalhes do campo de assinatura](images/signature-field-details.png)

Os administradores precisam adicionar o campo compartilhado existente *Desativar sobreposições de cofre (disable_vault_overlays__v)* e defini-lo como Ativo para todos os tipos de documento elegíveis para assinatura de Adobe. Opcionalmente, o campo pode ter uma segurança específica que permite que apenas os membros do grupo Adobe Sign Admin atualizem seu valor.

![Imagem de permitir ações do usuário do Adobe Sign](images/allow-adobe-sign-user-actions.png)

## Criar representações de documentos {#create-renditions}

Os administradores precisam criar um novo tipo de representação chamado *Adobe Sign Rendition (adobe_sign_rendition__c)*, que é usado pela integração do Vault para carregar documentos PDF assinados no Adobe Sign. A representação Adobe Sign deve ser declarada para cada tipo de documento elegível para a Assinatura de Adobe.

![Imagem de tipos de representação](images/rendition-type.png)

![Imagem de tipos de representação](images/edit-details-clinical-type.png)

## Configurar ações da Web {#web-actions}

A integração entre o Adobe Sign e o Vault exige que você crie e configure as duas ações da Web a seguir:

* **Criar Adobe Sign**: Ele cria ou exibe o Contrato da Adobe Sign.

   Tipo: Documento
Destino: Exibir no cofre
URL: <https://{integrationDomain}/adobe-sign-int/signature?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&sessionId=${Session.id}&vaultId=${Vault.Id>}

* **Cancelar Adobe Sign**: Cancela um contrato existente no Adobe Sign e reverte o estado de um documento para o estado inicial.

   Tipo: Documento
Destino: Exibir no cofre
URL: <https://{integrationDomain}/adobe-sign-int/cancel?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&sessionId=${Session.id}&vaultId=${Vault.Id>}

## Atualizar ciclo de vida do documento {#document-lifecycle}

Para cada tipo de documento qualificado para a Assinatura de Adobe, o ciclo de vida do documento correspondente deve ser atualizado adicionando novas funções e estados de ciclo de vida.

### Função do ciclo de vida {#lifecycle-role}

A função de aplicativo do Adobe Sign Admin deve ser adicionada em todos os ciclos de vida usados por documentos qualificados para a assinatura de Adobe. Essa função deve ser criada com as seguintes opções:

* Ativar Controle de Acesso Dinâmico
* Regras de compartilhamento de documentos que incluem apenas o Grupo de tipos de documento

![Imagem das funções de administrador do ciclo de vida](images/document-lifecycle-admin-role.png)

### Estados do ciclo de vida {#lifecycle-states}

O ciclo de vida do contrato da Adobe Sign tem os seguintes estados:

* RASCUNHO
* CRIAÇÃO ou DOCUMENTS_NOT_YET_PROCESSED
* OUT_FOR_SIGNATURE ou OUT_FOR_Approval
* ASSINADO ou APROVADO
* CANCELADO
* EXPIRADO

Quando um documento do Vault é enviado à Adobe Sign, seu estado deve corresponder ao estado em que o contrato está. Isso é feito adicionando os seguintes estados em cada ciclo de vida usado por documentos qualificados para assinatura de Adobe:

* **Antes da assinatura**  de Adobe (revisado): Este é um nome de espaço reservado para o estado do qual o documento pode ser enviado para o Adobe Sign. Com base no tipo de documento, ele pode ser estado Rascunho ou Revisado. A etiqueta de estado do documento pode ser personalizada de acordo com os requisitos do cliente. Antes do estado de Assinatura de Adobe, defina as seguintes duas ações do usuário:

   * Ação que altera o estado do documento para o estado *No Adobe Sign Draft*. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento para qualquer ciclo de vida. Se necessário, os critérios para essa ação podem ser definidos como &quot;Permitir ações de usuários da Adobe Sign é igual a Sim&quot;.
   * Ação que chama a Ação Web de &quot;Adobe Sign&quot;. Esse estado deve ter segurança que permita que a função de administrador da Adobe Sign: exibir documento, exibir conteúdo, editar campos, editar relacionamentos, baixar a origem, gerenciar representações visíveis e alterar o estado.

   ![Imagem do estado do ciclo de vida 1](images/lifecycle-state1.png)

* **No Adobe Sign Draft**: Este é um nome de espaço reservado para o estado que indica que o documento já foi carregado no Adobe Sign e que seu contrato está em um estado RASCUNHO. É um estado obrigatório. Esse estado deve indicar as seguintes cinco ações do usuário:

   * Ação que altera o estado do documento para *No estado Criação do Adobe Sign*. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento para qualquer ciclo de vida. Se necessário, os critérios para essa ação podem ser definidos como &quot;Permitir ações de usuários da Adobe Sign é igual a Sim&quot;.
   * Ação que altera o estado do documento para *No estado de Assinatura do Adobe*. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento para qualquer ciclo de vida. Se necessário, os critérios para essa ação podem ser definidos como &quot;Permitir ações de usuários da Adobe Sign é igual a Sim&quot;.
   * Ação que altera o estado do documento para o estado *Adobe Sign Canceled*. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento para qualquer ciclo de vida. Se necessário, os critérios para essa ação podem ser definidos como &quot;Permitir ações de usuários da Adobe Sign é igual a Sim&quot;.
   * Ação que chama a ação Web &quot;Adobe Sign&quot;.
   * Ação que chama a Ação da Web &quot;Cancelar Adobe Sign&quot;. Esse estado deve ter segurança que permita que a função de administrador da Adobe Sign: exibir documento, exibir conteúdo, editar campos, editar relacionamentos, baixar a origem, gerenciar representações visíveis e alterar o estado.

   ![Imagem do estado do ciclo de vida 2](images/lifecycle-state2.png)

* **Na criação** da Adobe Sign: Este é um nome de espaço reservado para o estado que indica que o documento já foi carregado no Adobe Sign e que seu contrato está no estado AUTORING ou DOCUMENTS_NOT_YET_PROCESSED. É um estado obrigatório. Esse estado deve ter quatro ações de usuário definidas:

   * Ação que altera o estado do documento para o estado Cancelado da Adobe Sign. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento, independentemente do ciclo de vida. Se necessário, os critérios para essa ação podem ser definidos como &quot;Permitir ações de usuários da Adobe Sign é igual a Sim&quot;.
   * Ação que altera o estado do documento para No estado de assinatura do Adobe. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento, independentemente do ciclo de vida. Se necessário, os critérios para essa ação podem ser definidos como &quot;Permitir ações de usuários da Adobe Sign é igual a Sim&quot;.
   * Ação que chama a Ação Web de &quot;Adobe Sign&quot;
   * Ação que chama a Ação da Web &quot;Cancelar Adobe Sign&quot;. Esse estado deve ter segurança que permita que a função de administrador da Adobe Sign: exibir documento, exibir conteúdo, editar campos, editar relacionamentos, baixar a origem, gerenciar representações visíveis e alterar o estado.

   ![Imagem do estado do ciclo de vida 3](images/lifecycle-state3.png)

* **Na assinatura** de Adobe: Este é um nome de espaço reservado para o estado que indica que o documento foi carregado no Adobe Sign e que seu contrato já foi enviado aos participantes (estado OUT_FOR_SIGNATURE ou OUT_FOR_Approval). É um estado obrigatório. Esse estado deve ter cinco ações de usuário definidas:

   * Ação que altera o estado do documento para o estado Cancelado da Adobe Sign. O estado de destino desta ação pode ser qualquer exigência do cliente e pode ser diferente para tipos diferentes. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento, independentemente do ciclo de vida. Se necessário, os critérios para essa ação podem ser definidos como &quot;Permitir ações de usuários da Adobe Sign é igual a Sim&quot;.
   * Ação que altera o estado do documento para o estado Adobe Sign Rejeitado. O estado de destino desta ação pode ser qualquer exigência do cliente e pode ser diferente para tipos diferentes. O nome desta ação do usuário deve ser o mesmo para todos os tipos de documento, independentemente do ciclo de vida. Se necessário, os critérios para essa ação podem ser definidos como &quot;Permitir ações de usuários da Adobe Sign é igual a Sim&quot;.
   * Ação que altera o estado do documento para o estado de Adobe Assinado. O estado de destino desta ação pode ser qualquer exigência do cliente e pode ser diferente para tipos diferentes. No entanto, o nome dessa ação do usuário deve ser o mesmo para todos os tipos de documento, independentemente do ciclo de vida. Se necessário, os critérios para essa ação podem ser definidos como &quot;Permitir ações de usuários da Adobe Sign é igual a Sim&quot;.
   * Ação que chama a Ação da Web *Adobe Sign*.
   * Ação que chama Ação da Web *Cancelar Adobe Sign*. Esse estado deve ter segurança que permita que a função de administrador da Adobe Sign: exibir documento, exibir conteúdo, editar campos, editar relacionamentos, baixar a origem, gerenciar representações visíveis e alterar o estado.

   ![Imagem do estado do ciclo de vida 4](images/lifecycle-state4.png)

* **Adobe assinado (aprovado)**: Este é um nome de espaço reservado para o estado que indica que o documento foi carregado no Adobe Sign e que seu contrato foi concluído (estado ASSINADO ou APROVADO). É um estado obrigatório e pode ser um estado do ciclo de vida existente, como Aprovado.
Esse estado não requer ações do usuário. Esse estado deve ter segurança que permita que a função de Administrador do Adobe Sign: exibir documentos, exibir conteúdo e editar campos.

O diagrama a seguir ilustra os mapeamentos entre o contrato da Adobe Sign e os estados do documento do Cofre, onde o estado &quot;Antes da assinatura de Adobe&quot; é Rascunho.

![Imagem de mapeamentos do Adobe Sign Vault](images/sign-vault-mappings.png)

## Configuração de Criar Grupo de Tipos de Documento e Função de Usuário  {#document-type-group-user-role}

### Criar grupo de tipos de documento {#create-document-type-group}

Os administradores precisam criar um novo registro de Grupo de tipos de documento chamado &quot;Documento Adobe Sign&quot;. Este grupo de tipos de documento é adicionado para todas as classificações de documento qualificadas para o processo Adobe Sign. Como a propriedade do grupo de tipos de documentos não é herdada do tipo para o subtipo nem do subtipo para o nível de classificação, ela deve ser definida para a classificação de cada documento elegível para o Adobe Sign.

![Imagem do tipo de documento](images/document-type.png)

### Criar Configuração de Função de Usuário {#create-user-role-setup}

Depois que o(s) ciclo(s) de vida estiver(em) configurado(s) corretamente, o sistema deve garantir que o usuário do Adobe Sign Admin seja adicionado pelo DAC para todos os documentos elegíveis ao processo Adobe Sign. Isso é feito criando o registro de Configuração de função de usuário apropriado que especifica:

* Grupo de tipos de documento como &#39;Documento Adobe Sign&#39;,
* Função do aplicativo como &#39;Função do administrador da Adobe Sign&#39; e
* Usuário de integração.

![Imagem da configuração da função de usuário](images/user-role-setup.png)

>[!NOTE]
>
>Se o objeto Configuração de função do usuário não contiver o campo que se refere ao objeto Grupo de tipos de documento, esse campo deverá ser adicionado.

## Ciclo de vida da implantação do pacote {#deployment-lifecycle}

### Ciclo geral de implantação {#general-deployment}

**Etapa 1.** Crie uma nova função de aplicativo chamada &#39;Função de administrador do Adobe Sign&#39;.

**Etapa 2.** Crie um novo grupo de tipos de documento chamado &#39;Documento Adobe Sign&#39;.

**Etapa 3.** Implante o pacote.

**Passo 4.** Crie um novo Grupo gerenciado pelo usuário chamado &#39;Grupo de administradores da Adobe Sign&#39;.

**Passo 5.** Crie um perfil de usuário de integração com o perfil de segurança &quot;Perfil de integração da Adobe Sign&quot; e atribua-o ao Grupo de administradores da Adobe Sign.

**Passo 6.** Atribua permissões de leitor para todos os perfis de segurança aos objetos de Assinatura, Assinatura e Evento de assinatura para usuários que exigem acesso ao histórico da Adobe Sign no Vault.

**Passo 7.** Defina a função de administrador da Adobe Sign no ciclo de vida de cada tipo de documento elegível para assinatura de Adobe. Para cada estado de ciclo de vida específico da Adobe Sign, essa função é adicionada e configurada com as permissões apropriadas.

**Passo 8.** Declare a representação da Adobe Sign para cada tipo de documento elegível para assinatura de Adobe.

**Passo 9.** Para cada tipo de documento qualificado para a Assinatura de Adobe, atualize o ciclo de vida do documento correspondente adicionando novas funções e estados de ciclo de vida.

**Passo 10.** Adicione o grupo de tipos de documento chamado &#39;Documento Adobe Sign&#39; para todas as classificações de documento qualificadas para o processo Adobe Sign.

**Passo 11.** Quando todas as configurações estiverem completas, o sistema deve garantir que o usuário do Adobe Sign Admin seja adicionado pelo DAC a todos os documentos qualificados para o processo Adobe Sign. Isso é feito criando o registro de Configuração da função de usuário apropriado que especifica o Grupo de tipos de documento como &quot;Documento Adobe Sign&quot;, Função do aplicativo como &quot;Função de administrador do Adobe Sign&quot; e um usuário de integração.

### Ciclo de vida de implantação específico {#specific-deployment}

**Etapa 1.** Crie uma nova função de aplicativo chamada &#39;Função de administrador do Adobe Sign&#39;.

**Etapa 2.** Crie um novo Grupo de Tipos de Documento chamado &#39;Documento Adobe Sign&#39;.

**Etapa 3.** Implante o pacote.

**Passo 4.** Crie um novo Grupo gerenciado pelo usuário chamado &#39;Grupo de administradores da Adobe Sign&#39;.

**Passo 5.** Crie um perfil de Usuário de integração com o perfil de Segurança chamado &#39;Perfil de integração da Adobe Sign&#39; e atribua ao Adobe Sign Admin Group.
