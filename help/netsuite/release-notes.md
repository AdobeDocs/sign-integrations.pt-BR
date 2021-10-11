---
title: Notas de versão do Adobe Sign for NetSuite
description: Saiba mais sobre os novos recursos e alterações incluídos na versão atual da integração da Adobe Sign com o NetSuite.
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 6317723e-447a-4506-a621-4d967bdd6561
source-git-commit: f8d0bc748872e675dc1c638eb4050efe9e3147ef
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 5%

---

# Notas de versão do Adobe Sign for NetSuite

## Atualização para o pacote v4.0.4

4.0.4 é totalmente adaptado para usar domínios específicos da conta para todo o tráfego recém-gerado.

O ícone do Adobe Sign foi atualizado para o novo gráfico.

## Versões anteriores

### Adobe Sign para NetSuite 4.0.4

4.0.4 é totalmente adaptado para usar domínios específicos da conta para todo o tráfego recém-gerado.

O ícone do Adobe Sign foi atualizado para o novo gráfico.

### Adobe Sign para NetSuite 4.0.2

Mudança de marca para **Adobe Sign** (de *Serviços eSign da Adobe Document Cloud*)\
Agora você vê *Adobe Sign* onde anteriormente via *Serviços de eSign da Adobe* como evidência da mudança de marca.

### Adobe Sign para NetSuite 4.0.1

Devido a um erro de regressão de API introduzido quando o NetSuite executou a atualização da plataforma, foi lançado um novo pacote (v4.0.1).

Os clientes são incentivados a atualizar para o pacote mais recente.

### Adobe Sign para NetSuite 4.0

**Provisionamento automático adicionado de usuários por meio do NetSuite**

Uma nova preferência personalizada foi adicionada para v4.0. Quando ativado, os usuários que enviam contratos no NetSuite são provisionados automaticamente com uma conta de usuário dos serviços eSign da Adobe Document Cloud.

**Certificado com &quot;Built for NetSuite&quot;**

Esta versão alcançou a certificação &quot;Built for NetSuite&quot; e atende a todas as práticas recomendadas de design mais recentes do NetSuite.

**Remarca para os serviços eSign da Adobe Document Cloud (da EchoSign)**

Agora você vê os Serviços eSign da Adobe Document Cloud (ou os Serviços eSign da Adobe) onde anteriormente via a Adobe EchoSign como evidência da mudança de marca.

**Segurança aprimorada implementada com OAuth**

Para melhorar a segurança dos dados, os serviços eSign agora usam o OAuth 2.0 para autenticar sua conta de serviços eSign da Adobe Document Cloud no NetSuite. Esse novo protocolo permite que o NetSuite fale com os serviços eSign sem solicitar sua senha dos serviços eSign. Já que informações confidenciais não está sendo compartilhadas diretamente entre os aplicativos, sua conta tem menos probabilidade de ficar comprometida. Essa melhoria não afeta sua implementação, mas você deve fazer uma configuração única para autorizar seu pacote NetSuite a se comunicar com a Adobe Document Cloud. Isso é feito durante o processo de instalação. Para clientes que atualizam de uma versão anterior do pacote — v3.5.9 e anterior — a chave da API usada anteriormente é substituída por um token OAuth gerado durante o processo de autorização.

**Migração dos serviços eSign de APIs SOAP para APIs REST**

Para melhorar a eficiência, a flexibilidade e a velocidade de processamento, os serviços eSign da Adobe Document Cloud e, consequentemente, a integração v4.0 para NetSuite, migraram de APIs baseadas em SOAP para APIs baseadas em REST.

### Adobe Sign para NetSuite 3.0

**Funções avançadas de participante - Aprovador**

* Um ou mais destinatários podem ser marcados como aprovadores em um contrato
* Os aprovadores devem revisar e aprovar o documento
* Os aprovadores também podem ser solicitados a preencher os dados do contrato antes de aprovar

**Visualizar documento ou arrastar e soltar campos de formulário antes de enviar**

Visualizar o contrato ou arrastar e soltar campos de formulário antes de enviar para assinatura

**Enviar lembrete ao signatário atual**

Enviar lembrete imediato ao signatário atual

**Políticas de autenticação avançadas do signatário**

* **Autenticação baseada em conhecimento:** responda perguntas para verificar a identidade do signatário
   * Exige que os signatários comprovem sua identidade respondendo a perguntas feitas em centenas de bancos de dados públicos e comerciais
   * O nome na assinatura é retirado do nome autenticado do usuário e não pode ser alterado no momento da assinatura
   * Desenvolvido pela RSA
   * O uso do KBA é limitado por conta, por mês. Entre em contato com o setor de Vendas para obter mais informações.

* **Identidade da Web:** faça logon com Facebook, LinkedIn, Google ou outro serviço da Web de terceiros antes de assinar.

   * O signatário só pode assinar depois de verificar sua identidade usando um serviço Web de terceiros.
   * O nome na assinatura é retirado do serviço Web pro!le do usuário e não pode ser alterado no momento da assinatura
   * A trilha de auditoria captura detalhes de verificação de identidade

* **Senha única**
   * Aplique métodos de autenticação para signatários internos ou externos ou todos os signatários. Os signatários externos devem usar uma senha ou usar a autenticação baseada em conhecimento enquanto os signatários internos não

**Preferências personalizadas adicionais**

* Adicionar PDF assinado como um link para o URL ou como anexo hospedado no NetSuite
* Adicionar trilha de auditoria ao registro do contrato um contrato$er é assinado
* Use o contato de transação como signatário por padrão, em vez do email do Cliente
* Conceder aos remetentes a opção de marcar os destinatários como Aprovadores

**Arquivos de transação**

Você pode selecionar arquivos para anexar da transação atual com a nova lista suspensa &quot;Arquivos de transação&quot;.

**Certificação do Adobe PDF para todos os documentos do EchoSign**

* Todos os arquivos de PDF enviados ou baixados do EchoSign são certificados com um certificado digital da Adobe EchoSign
* Acrobat ou Reader exibe a certificação que garante que o documento não foi adulterado para obter confiança adicional e tranquilidade

**Coletar documentos de suporte**

* Os remetentes podem coletar documentos de suporte adicionais dos signatários durante a assinatura, como uma licença de driver, um certificado comercial e muito mais.
* Os documentos coletados tornam-se parte do registro oficial do contrato assinado

**Campos de dos condicionais**

* Definir lógica condicional para campos de contrato
* As condições podem ser baseadas em valores para um ou mais campos no contrato
* As condições podem ser eliminadas!por meio da interface do usuário de criação de formulários de arrastar e soltar ou por meio de tags de texto
* O signatário é apresentado com os campos apropriados ao assinar um documento com base nas condições de desistência

**Melhorias adicionais dos campos de formulário do EchoSign**

* Menus suspensos
* Máscara de campo
* Botões de opção
* Criar tags de texto mais curtas para manter a estrutura do documento
