---
title: Verificatie Details van Azure Maps weer geven
description: Gebruik de Azure Portal om de verificatie Details van Azure Maps weer te geven.
author: anastasia-ms
ms.author: v-stharr
ms.date: 06/17/2020
ms.topic: include
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.openlocfilehash: a6ffcbf5a8c36958dd3ea74de4d826fe25a1139c
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/09/2020
ms.locfileid: "87126449"
---
U kunt de verificatie Details van het Azure Maps account bekijken in de Azure Portal. In uw account selecteert u in het menu **instellingen** de optie **verificatie**.

![Verificatie gegevens](../media/how-to-manage-authentication/how-to-view-auth.png)

Zodra een Azure Maps account is gemaakt, is de Azure Maps `x-ms-client-id` waarde aanwezig op de pagina Azure Portal verificatie Details. Deze waarde vertegenwoordigt het account dat wordt gebruikt voor REST API aanvragen. Deze waarde moet worden opgeslagen in de configuratie van de toepassing en worden opgehaald voordat u HTTP-aanvragen maakt wanneer u Azure AD-verificatie gebruikt met Azure Maps.
