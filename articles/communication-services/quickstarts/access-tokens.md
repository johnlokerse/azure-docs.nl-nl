---
title: Snelstart - Toegangstoken maken en beheren
titleSuffix: An Azure Communication Services quickstart
description: Meer informatie over het beheren van identiteits- en toegangstokens met behulp van de Azure Communication Services Administration-clientbibliotheek.
author: tomaschladek
manager: nmurav
services: azure-communication-services
ms.author: tchladek
ms.date: 08/20/2020
ms.topic: quickstart
ms.service: azure-communication-services
zone_pivot_groups: acs-js-csharp-java-python
ms.openlocfilehash: b67d0808643797d88628b626403c1b9d97cf1cad
ms.sourcegitcommit: 4bee52a3601b226cfc4e6eac71c1cb3b4b0eafe2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/11/2020
ms.locfileid: "94506219"
---
# <a name="quickstart-create-and-manage-access-tokens"></a>Quickstart: Toegangstokens maken en beheren

[!INCLUDE [Public Preview Notice](../includes/public-preview-include.md)]

Ga aan de slag met Azure Communication Services door de clientbibliotheek van Communications Services-beheer te gebruiken. Hiermee kunt u identiteiten maken en uw toegangstokens beheren. De identiteit geeft de entiteit weer van uw toepassing in de Azure Communication Service (bijvoorbeeld gebruiker of apparaat). Met toegangstokens kunt u uw chat- en aanroep-clientbibliotheken rechtstreeks verifiëren tegen Azure Communication Services. Het wordt aanbevolen om toegangstokens te genereren voor een service aan de serverzijde. Toegangstokens worden vervolgens gebruikt voor het initialiseren van de Communication Services-clientbibliotheken op clientapparaten.

Prijzen die in de afbeeldingen in deze zelfstudie worden getoond, zijn alleen bedoeld voor demonstratiedoeleinden.

::: zone pivot="programming-language-csharp"
[!INCLUDE [.NET](./includes/user-access-token-net.md)]
::: zone-end

::: zone pivot="programming-language-javascript"
[!INCLUDE [JavaScript](./includes/user-access-token-js.md)]
::: zone-end

::: zone pivot="programming-language-python"
[!INCLUDE [Python](./includes/user-access-token-python.md)]
::: zone-end

::: zone pivot="programming-language-java"
[!INCLUDE [Java](./includes/user-access-token-java.md)]
::: zone-end

De uitvoer van de app beschrijft elke actie die is voltooid:
<!---cSpell:disable --->
```console
Azure Communication Services - Access Tokens Quickstart

Created an identity: 8:acs:4ccc92c8-9815-4422-bddc-ceea181dc774_00000006-19e0-2727-80f5-8b3a0d003502

Issued a access token with 'voip' scope for identity with ID: 8:acs:4ccc92c8-9815-4422-bddc-ceea181dc774_00000006-19e0-2727-80f5-8b3a0d003502:
<token signature here>

Successfully deleted the identity with ID: 8:acs:4ccc92c8-9815-4422-bddc-ceea181dc774_00000006-19e0-2727-80f5-8b3a0d003502

Deleted the identity with ID: 8:acs:4ccc92c8-9815-4422-bddc-ceea181dc774_00000006-19e0-2727-80f5-8b3a0d003502
```
<!---cSpell:enable --->

## <a name="clean-up-resources"></a>Resources opschonen

Als u een Communication Services-abonnement wilt opschonen en verwijderen, kunt u de resource of resourcegroep verwijderen. Als u de resourcegroep verwijdert, worden ook alle bijbehorende resources verwijderd. Meer informatie over het [opschonen van resources](./create-communication-resource.md#clean-up-resources).


## <a name="next-steps"></a>Volgende stappen

In deze snelstart hebt u de volgende zaken geleerd:

> [!div class="checklist"]
> * Identiteiten beheren
> * Toegangstokens uitgeven
> * De clientbibliotheek voor Communication Services-beheer gebruiken


> [!div class="nextstepaction"]
> [Spraakoproep aan uw app toevoegen](./voice-video-calling/getting-started-with-calling.md)

U kunt ook het volgende doen:

 - [Meer informatie over verificatie](../concepts/authentication.md)
 - [Chat aan uw app toevoegen](./chat/get-started.md)
 - [Meer informatie over de client -en serverarchitectuur](../concepts/client-and-server-architecture.md)
 