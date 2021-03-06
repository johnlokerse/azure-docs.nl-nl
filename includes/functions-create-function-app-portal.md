---
title: bestand opnemen
description: bestand opnemen
services: functions
author: ggailey777
ms.service: azure-functions
ms.topic: include
ms.date: 03/04/2020
ms.author: glenga
ms.custom: include file
ms.openlocfilehash: 439b312050f657566026a36c145e7b6dd5cc9bad
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/09/2020
ms.locfileid: "83116322"
---
1. Selecteer vanuit het menu van Azure Portal of op de **startpagina** de optie **Een resource maken**.

1. Selecteer op de pagina **Nieuw** **Reken** > **functie-app**.

1. Op de pagina **Basics** gebruikt u de instellingen voor de functie-app zoals in de volgende tabel wordt vermeld.

    | Instelling      | Voorgestelde waarde  | Beschrijving |
    | ------------ | ---------------- | ----------- |
    | **Abonnement** | Uw abonnement | Het abonnement waarmee deze nieuwe functie-app is gemaakt. |
    | **[Resourcegroep](../articles/azure-resource-manager/management/overview.md)** |  *myResourceGroup* | Naam voor de nieuwe resourcegroep waarin uw functie-app moet worden gemaakt. |
    | **Naam van de functie-app** | Wereldwijd unieke naam | Naam waarmee uw nieuwe functie-app wordt aangeduid. Geldige tekens zijn `a-z` (hoofdlettergevoelig), `0-9` en `-`.  |
    |**Publiceren**| Code | Optie voor het publiceren van codebestanden of een Docker-container. |
    | **Runtimestack** | Voorkeurstaal | Kies een runtime die uw favoriete functieprogrammeertaal ondersteunt. Kies **.NET Core** voor C#- en F#-functies. |
    |**Versie**| Versienummer | Kies de versie van uw geïnstalleerde runtime.  |
    |**Regio**| Voorkeursregio | Kies een [regio](https://azure.microsoft.com/regions/) in de buurt of in de buurt van andere services die door uw functie worden gebruikt. |

    ![Basisbeginselen](./media/functions-create-function-app-portal/function-app-create-basics.png)

1. Selecteer **Volgende : Hosting**. Voer op de pagina **Hosting** de volgende instellingen in.

    | Instelling      | Voorgestelde waarde  | Beschrijving |
    | ------------ | ---------------- | ----------- |
    | **[Opslagaccount](../articles/storage/common/storage-account-create.md)** |  Wereldwijd unieke naam |  Maak een opslagaccount die wordt gebruikt door uw functie-app. Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en kunnen alleen cijfers en kleine letters bevatten. U kunt ook een bestaand account gebruiken dat voldoet aan de [vereisten voor een opslagaccount](../articles/azure-functions/functions-scale.md#storage-account-requirements). |
    |**Besturingssysteem**| Voorkeurbesturingssysteem | Er wordt vooraf een besturingssysteem geselecteerd voor u op basis van de selectie van de runtimestack, maar u kunt de instelling wijzigen, indien nodig. |
    | **[Plannen](../articles/azure-functions/functions-scale.md)** | **Verbruik (serverloos)** | Hostingabonnement dat definieert hoe resources worden toegewezen aan uw functie-app. In het standaard **Verbruiksabonnement** worden resources dynamisch toegevoegd zoals door uw functies wordt vereist. Met hosten [zonder server](https://azure.microsoft.com/overview/serverless-computing/) betaalt u alleen voor de tijd dat uw functies actief zijn. Wanneer u in een App Service-plan uitvoert, moet u het [Schalen van uw functie-app](../articles/azure-functions/functions-scale.md) beheren.  |

    ![Hosting](./media/functions-create-function-app-portal/function-app-create-hosting.png)

1. Selecteer **Volgende : Bewaking**. Voer op de pagina **Bewaking** de volgende instellingen in.

    | Instelling      | Voorgestelde waarde  | Beschrijving |
    | ------------ | ---------------- | ----------- |
    | **[Application Insights](../articles/azure-functions/functions-monitoring.md)** | Standaard | Hiermee maakt u een Application Insights-resource van dezelfde *app-naam* in de dichtstbijzijnde ondersteunde regio. Door deze instelling uit te vouwen of **Nieuwe maken** te selecteren, kunt u de naam van Application Insights wijzigen of een andere regio kiezen in een [Azure-geografie](https://azure.microsoft.com/global-infrastructure/geographies/) waar u uw gegevens wilt opslaan. |

    ![Bewaking](./media/functions-create-function-app-portal/function-app-create-monitoring.png)

1. Selecteer **Beoordelen + maken** om de selecties van appconfiguratie te controleren.

1. Controleer uw instellingen op de pagina **Beoordelen en maken** en selecteer vervolgens **Maken** om de functie-app in te richten en te implementeren.

1. Selecteer het **Meldingspictogram** in de rechterbovenhoek van de portal en zoek het bericht **Implementatie voltooid**.

1. Selecteer **Naar de resource gaan** om uw nieuwe functie-app te bekijken. U kunt ook **Vastmaken aan dashboard** selecteren. Vastmaken maakt het gemakkelijker om terug te gaan naar deze functie-app-resource vanuit uw dashboard.

    ![Implementatiemelding](./media/functions-create-function-app-portal/function-app-create-notification2.png)