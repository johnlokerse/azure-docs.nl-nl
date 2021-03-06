---
title: Een OpenAPI-specificatie importeren met Azure Portal | Microsoft Docs
description: Leer hoe u een OpenAPI-specificatie importeert met API Management en de API vervolgens test in de Azure- en ontwikkelaarsportal.
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 04/20/2020
ms.author: apimpm
ms.openlocfilehash: 05295efec3d7651c3a77dd5ad6e2c72b57a6c5a3
ms.sourcegitcommit: 4b76c284eb3d2b81b103430371a10abb912a83f4
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/01/2020
ms.locfileid: "93146753"
---
# <a name="import-an-openapi-specification"></a>Een OpenAPI-specificatie importeren

In dit artikel ziet u hoe u een back-end-API met de naam OpenAPI-specificatie kunt importeren die zich bevindt in https://conferenceapi.azurewebsites.net?format=json. Deze back-end-API wordt geleverd door Microsoft en gehost in Azure. In het artikel wordt ook uitgelegd hoe u de APIM-API kunt testen.

In dit artikel leert u het volgende:

> [!div class="checklist"]
> * Een back-end-API met de naam OpenAPI-specificatie importeren
> * De API testen in Azure Portal
> * De API testen in de ontwikkelaarsportal

## <a name="prerequisites"></a>Vereisten

Voltooi de volgende quickstart: [Een Azure API Management-exemplaar maken](get-started-create-service-instance.md)

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <a name="import-and-publish-a-back-end-api"></a><a name="create-api"> </a>Een back-end-API importeren en publiceren

1. Navigeer naar uw API Management-service in de Azure Portal en selecteer **API's** in het menu.
2. Selecteer **OpenAPI-specificatie** in de lijst **Een nieuwe API toevoegen** .

    ![OpenAPI-specificatie](./media/import-api-from-oas/oas-api.png)
3. Voer API-instellingen in. U kunt de waarden instellen tijdens het maken of later configureren door naar het tabblad **Instellingen** te gaan. De instellingen worden beschreven in de zelfstudie [Uw eerste API importeren en publiceren](import-and-publish.md#import-and-publish-a-backend-api).
4. Selecteer **Maken** .

> [!NOTE]
> De API-importbeperkingen staan in [een ander artikel](api-management-api-import-restrictions.md).

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-append-apis.md)]

[!INCLUDE [api-management-define-api-topics.md](../../includes/api-management-define-api-topics.md)]

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Een gepubliceerde API transformeren en beveiligen](transform-api.md)
