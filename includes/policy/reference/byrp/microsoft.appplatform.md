---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 11/17/2020
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: 2b46aa4c782020c8b9ef3d2534d120b41b88018c
ms.sourcegitcommit: c2dd51aeaec24cd18f2e4e77d268de5bcc89e4a7
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94736114"
---
|Naam<br /><sub>(Azure-portal)</sub> |Beschrijving |Gevolg(en) |Versie<br /><sub>(GitHub)</sub> |
|---|---|---|---|
|[Azure Spring Cloud-instanties controleren waar gedistribueerde tracering niet is ingeschakeld](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0f2d8593-4667-4932-acca-6a9f187af109) |Met gedistribueerde traceringshulpprogramma's in Azure Spring Cloud worden foutopsporing en controle van de complexe verbindingen mogelijk tussen microservices in een toepassing. Gedistribueerde traceringshulpprogramma's moeten zijn ingeschakeld en goed werken. |Controle, uitgeschakeld |[1.0.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/App%20Platform/Spring_DistributedTracing_Audit.json) |
|[Azure Spring Cloud moet netwerkinjectie gebruiken](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Faf35e2a4-ef96-44e7-a9ae-853dd97032c4) |Azure Spring Cloud-exemplaren moeten om de volgende redenen virtuele netwerkinjectie gebruiken: 1. Azure Spring Cloud isoleren van internet. 2. Azure Spring Cloud-interactie met systemen inschakelen in on-premises datacentrums of Azure-services in andere virtuele netwerken. 3. Klanten in staat stellen de binnenkomende en uitgaande netwerkcommunicatie voor Azure Spring Cloud te beheren. |Controleren, uitgeschakeld, weigeren |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/App%20Platform/Spring_VNETEnabled_Audit.json) |
