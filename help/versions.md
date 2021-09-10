---
title: Integrações Adobe Sign — versões e ciclo de vida do produto
description: Saiba mais sobre as versões do Adobe Sign Integrations e o ciclo de vida do suporte
audience: External
products: Adobe Sign
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: c1f22848-7951-4066-84d4-f8cf6c2f3a6f
source-git-commit: 30cb79b6856c7b623dc5118b4aa40193bf749220
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Versões de produto e ciclo de vida {#version}

A convenção de controle de versão da Adobe Sign e o ciclo de vida de suporte para serviços integrados se alinham a outros produtos de Adobe que você possa conhecer.

## Números de versão

A versão do pacote usa um sistema de numeração de três partes para identificar o número de compilação sequencial da versão disponibilizada e a importação relativa da atualização em termos de conteúdo novo ou em alteração.

O número da versão segue este padrão: N.m.p

Onde, N = Versão principal; m = Versão secundária; p = Versão corrigida.

Por exemplo, uma versão 23.2.1 do pacote de integração indica um status de versão de:

* Versão principal: 23
* Versão secundária: 2
* Versão do patch: 1

À medida que os engenheiros desenvolvem novas &quot;construções&quot; do pacote, eles incrementam o número da versão de acordo com a natureza das atualizações do código.

* As mudanças nas versões principais envolvem uma adição significativa nos recursos ou uma mudança importante nos sistemas centrais.
* As atualizações de versão secundária incluem atualizações de recursos menores e patches de segurança. A Adobe Sign pode exigir uma atualização para a versão corrigida mais recente em caso de atualizações de segurança ou para tratar de um item reportado.
* As versões de correção são quase exclusivamente correções de erros e ajustes de interface do usuário

>[!NOTE]
>
>Todas as versões não são lançadas ao público, pois o produto é iterado no desenvolvimento. Portanto, pode haver saltos significativos na versão do patch entre as versões.

Os administradores devem manter a versão atualizada para garantir que a conta tenha acesso total a todos os recursos e todos os problemas de segurança conhecidos sejam corrigidos. A Adobe Sign pode exigir uma atualização para a versão corrigida mais recente em caso de problemas de segurança ou para solucionar problemas críticos do sistema.

## Ciclo de vida do suporte da versão

O ciclo de vida do suporte da versão de um produto de integração da Adobe Sign é definido com base na versão principal do pacote e indica o período de tempo que a Adobe Sign está suportando ativamente a versão individual da integração.

A Adobe Sign oferece suporte à versão atual de um pacote e às duas versões principais anteriores (inclusive com todas as atualizações de correções e menores relacionadas). As versões principais são apresentadas da seguinte forma:

* Versão atual (N): a versão principal mais recente do pacote
* Versão anterior (N-1): uma versão principal anterior à versão mais recente
* Última versão compatível (N-2): duas versões principais anteriores à versão atual

Por exemplo, se a versão disponível atual do pacote for 23.2.1, então:

* A versão principal atual (N) é 23
* A versão principal anterior (N-1) deste pacote é 22
* A última versão principal compatível (N-2) deste pacote é 21
* Não há suporte para todas as versões anteriores a 21.0.0

![Gráfico de versão](images/version_chart.png)

## Ciclo do serviço de versão

O ciclo de vida do serviço da versão define o escopo completo de quando o serviço é utilizável. A linha do tempo corresponde ao ciclo de vida do suporte da versão com a adição de um período de carência de 90, dias que permite aos clientes concluir a atualização.

* Durante o período de carência de uma versão não compatível, o suporte é fornecido apenas para atualizar para uma versão mais recente, e não para manter uma versão não compatível
* Após o período de carência, a versão fica sem serviço

* O Adobe Sign não aceita solicitações de versões que estão fora de serviço
* Depois que a integração for atualizada para a versão atual, as comunicações entre o Adobe Sign e a integração serão retomadas normalmente

![Período de inatividade](images/shutdown_period.png)

Entre em contato com o revendedor ou com o suporte ao cliente se tiver dúvidas.
