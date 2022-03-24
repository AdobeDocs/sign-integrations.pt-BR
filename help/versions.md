---
title: Versões e ciclo de vida do produto de integrações da Adobe Sign
description: Saiba mais sobre as versões das integrações da Adobe Sign e o ciclo de vida do suporte
audience: External
products: Adobe Sign
type: Documentation
solution: Acrobat Sign, Adobe Sign
role: User, Developer
topic: Integrations
exl-id: c1f22848-7951-4066-84d4-f8cf6c2f3a6f
source-git-commit: b326a9afa2c16333d390cac3b30a2c7c741a4360
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 40%

---

# Versões e ciclo de vida do produto {#version}

A convenção de controle de versão e o ciclo de vida do suporte do Adobe Sign para serviços integrados se alinha a outros produtos Adobe com os quais você pode estar familiarizado.

## Números de versão

A versão do pacote usa um sistema de numeração de três partes para identificar o número de compilação sequencial da versão disponibilizada e a importação relativa da atualização em termos de conteúdo novo ou com alteração.

O número da versão segue este padrão: N.m.p.

Em que N = versão principal; m = Versão secundária; p = Versão corrigida.

Por exemplo, uma versão do pacote de integração 23.2.1 indica um status de versão de:

* Versão principal: 23
* Versão secundária: 2
* Versão do patch: 1

À medida que os engenheiros desenvolvem novas &quot;compilações&quot; do pacote, eles incrementam o número da versão de acordo com a natureza das atualizações do código.

* As alterações na versão principal envolvem uma adição significativa nos recursos ou uma alteração importante nos sistemas principais.
* As atualizações da versão secundária incluem atualizações de recursos menores e correções de segurança. O Adobe Sign pode exigir uma atualização para a versão corrigida mais recente caso haja atualizações de segurança ou para solucionar um item relatado.
* As versões de correção são quase exclusivamente correções de erros e ajustes de interface do usuário

>[!NOTE]
>
>Todas as versões não são disponibilizadas ao público à medida que o produto sai e volta para o desenvolvimento. Portanto, pode haver saltos significativos na versão de correção entre as versões.

Os administradores devem manter suas versões atualizadas para garantir que a conta tenha acesso total a todos os recursos e todos os problemas de segurança conhecidos sejam corrigidos. A Adobe Sign pode exigir uma atualização para a versão corrigida mais recente, caso haja um problema de segurança ou para solucionar um problema crítico do sistema.

## Ciclo de vida do suporte da versão

O ciclo de vida do suporte da versão de um produto de integração do Adobe Sign é definido com base na versão principal do pacote e indica o período de tempo em que o Adobe Sign está oferecendo suporte ativo à versão individual da integração.

O Adobe Sign é compatível com a versão atual de um pacote e as duas versões principais anteriores (inclusive com todas as atualizações secundárias e de correções relacionadas). As versões principais são apresentadas da seguinte forma:

* Versão atual (N): a versão principal mais recente do pacote
* Versão anterior (N-1): uma versão principal anterior à versão mais recente
* Última versão compatível (N-2): duas versões principais anteriores à versão atual

Por exemplo, se a versão atual disponível do pacote for 23.2.1, então:

* A versão principal atual (N) é 23
* A versão principal anterior (N-1) deste pacote é 22
* A última versão principal compatível (N-2) deste pacote é 21
* Não há suporte para todas as versões anteriores a 21.0.0

![Gráfico de versão](images/version_chart.png)

## Ciclo de vida do serviço de versão

O ciclo de vida do serviço da versão define o escopo completo de quando o serviço é utilizável. A linha do tempo corresponde ao ciclo de vida do suporte da versão com a adição de um período de carência de 90, dias que permite aos clientes concluir a atualização.

* Durante o período de carência de uma versão não compatível, o suporte é fornecido apenas para atualizar para uma versão mais recente, e não para manter uma versão não compatível
* Após o período de carência, a versão fica fora de serviço

* O Adobe Sign não aceita solicitações de versões que estão fora de serviço
* Depois que a integração for atualizada para a versão atual, as comunicações entre o Adobe Sign e a integração serão retomadas normalmente

![Período de inatividade](images/shutdown_period.png)

Entre em contato com o revendedor ou com o suporte ao cliente se tiver dúvidas.
