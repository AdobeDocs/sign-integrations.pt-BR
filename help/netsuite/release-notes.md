---
title: Notas de versão do Adobe Sign para NetSuite
description: Conheça os novos recursos e as alterações incluídas na versão atual da integração do Adobe Sign para NetSuite.
type: Documentation
solution: Acrobat Sign, Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 6317723e-447a-4506-a621-4d967bdd6561
source-git-commit: b326a9afa2c16333d390cac3b30a2c7c741a4360
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 5%

---

# Notas de versão do Adobe Sign para NetSuite

## Atualização do pacote v4.0.4

4.0.4 está totalmente adaptado para usar domínios específicos da conta para todo o tráfego recém-gerado.

O ícone do Adobe Sign foi atualizado para o novo gráfico.

## Versões anteriores

### Adobe Sign para NetSuite 4.0.4

4.0.4 está totalmente adaptado para usar domínios específicos da conta para todo o tráfego recém-gerado.

O ícone do Adobe Sign foi atualizado para o novo gráfico.

### Adobe Sign para NetSuite 4.0.2

Renomeado para **Adobe Sign** (de *Serviços eSign da Adobe Document Cloud*)\
Agora você vê *Adobe Sign* onde você viu anteriormente *Serviços eSign do Adobe* como prova da mudança de marca.

### Adobe Sign para NetSuite 4.0.1

Devido a um erro de regressão da API introduzido quando o NetSuite executou sua atualização de plataforma, um novo pacote (v4.0.1) foi lançado.

Recomenda-se que os clientes atualizem para o pacote mais recente.

### Adobe Sign para NetSuite 4.0

**Adicionado provisionamento automático de usuários por meio do NetSuite**

Uma nova preferência personalizada foi adicionada para v4.0. Quando ativada, os usuários que enviam contratos no NetSuite são provisionados automaticamente com uma conta de usuário dos serviços eSign da Adobe Document Cloud.

**Certificado com &quot;Criado para NetSuite&quot;**

Esta versão obteve a certificação &quot;Built for NetSuite&quot; e atende a todas as práticas recomendadas de design mais recentes do NetSuite.

**Renomeado para os serviços eSign da Adobe Document Cloud (do EchoSign)**

Agora, você verá os serviços eSign da Adobe Document Cloud (ou Adobe eSign Services para abreviar), onde anteriormente você via o Adobe EchoSign como evidência da mudança de marca.

**Segurança aprimorada implementada com OAuth**

Para melhorar a segurança dos dados, os serviços eSign agora usam o OAuth 2.0 para autenticar sua conta de serviços eSign da Adobe Document Cloud dentro do NetSuite. Esse novo protocolo permite que o NetSuite se comunique com os serviços eSign sem solicitar sua senha para esses serviços. Já que informações confidenciais não está sendo compartilhadas diretamente entre os aplicativos, sua conta tem menos probabilidade de ficar comprometida. Essa melhoria não afeta sua implementação, mas você deve fazer uma configuração única para autorizar que seu pacote NetSuite se comunique com o Adobe Document Cloud. Isso é feito durante o processo de instalação. Para clientes que atualizam de uma versão anterior do pacote — v3.5.9 e anterior — a chave de API anteriormente usada é substituída por um token OAuth gerado durante o processo de autorização.

**Migração dos serviços eSign de APIs SOAP para APIs REST**

Para melhorar a eficiência, a flexibilidade e a velocidade de processamento, os serviços eSign da Adobe Document Cloud e, consequentemente, a integração v4.0 para NetSuite, migraram de APIs baseadas em SOAP para APIs baseadas em REST.

### Adobe Sign para NetSuite 3.0

**Funções avançadas de participante - aprovador**

* Um ou mais destinatários podem ser marcados como aprovadores em um contrato
* Os aprovadores devem revisar e aprovar o documento
* Os aprovadores também podem ser solicitados a preencher os dados do contrato antes de aprovarem

**Visualizar documentos ou arrastar e soltar campos de formulário antes de enviar**

Visualize o contrato ou arraste e solte os campos do formulário antes de enviar para assinatura

**Enviar lembrete ao signatário atual**

Enviar lembrete imediato ao signatário atual

**Políticas de autenticação avançada de signatários**

* **Autenticação baseada em conhecimento:** Responda às perguntas para verificar a identidade do signatário
   * Exige que os signatários provem sua identidade respondendo a perguntas de centenas de bancos de dados públicos e comerciais
   * O nome na assinatura é obtido do nome autenticado do usuário e não pode ser alterado no momento da assinatura
   * Desenvolvido pela RSA
   * O uso do KBA é limitado por conta, por mês. Entre em contato com o setor de Vendas para obter mais informações.

* **Identidade Web:** Faça logon com o Facebook, o LinkedIn, o Google ou outros serviços da Web de terceiros antes de assinar.

   * O signatário só pode assinar depois de verificar sua identidade usando um serviço Web de terceiros.
   * O nome na assinatura é obtido do serviço Web do usuário pro!le e não pode ser alterado no momento da assinatura
   * A trilha de auditoria captura detalhes da verificação de identidade

* **Senha ocasional**
   * Aplique métodos de autenticação para signatários internos ou externos ou para todos os signatários. Os signatários externos devem usar uma senha ou a Autenticação baseada em conhecimento, mas os signatários internos não

**Preferências personalizadas adicionais**

* Adicionar PDF assinado como um link para o URL ou como anexo hospedado no NetSuite
* Adicionar trilha de auditoria ao registro de contrato a$er contrato assinado
* Usar o contato da transação como signatário por padrão, em vez de email do Cliente
* Conceder aos remetentes a opção de marcar destinatários como aprovadores

**Arquivos de Transação**

Você pode selecionar arquivos para anexar da transação atual com a nova lista suspensa &quot;Arquivos de transação&quot;.

**Certificação do Adobe PDF para todos os documentos do EchoSign**

* Todos os arquivos PDF enviados ou baixados do EchoSign são certificados com um certificado digital da Adobe EchoSign
* O Acrobat ou o Reader exibe a certificação que garante que o documento não foi adulterado para proporcionar confiança e tranquilidade adicionais

**Coletar documentos de suporte**

* Os remetentes podem coletar documentos de suporte adicionais dos signatários durante a assinatura, como CNH, certificado comercial e muito mais.
* Os documentos coletados tornam-se parte do registro oficial do contrato assinado

**Campos de dos condicionais**

* Definir lógica condicional para campos de contrato
* As condições podem ser baseadas em valores para um ou mais campos no contrato
* As condições podem ser removidas por meio da interface do usuário de criação de formulários com a função arrastar e soltar ou por meio de tags de texto
* Ao assinar um documento com base nas condições de!ned, o signatário verá os campos apropriados

**Melhorias adicionais dos campos de formulário do EchoSign**

* Menus suspensos
* Mascaramento de campo
* Botões de opção
* Criar tags de texto menores para manter a estrutura do documento
