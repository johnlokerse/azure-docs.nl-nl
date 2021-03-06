---
title: Azure-abonnement als Event Grid bron
description: Hierin worden de eigenschappen beschreven die worden verschaft voor abonnements gebeurtenissen met Azure Event Grid
ms.topic: reference
ms.date: 07/07/2020
ms.openlocfilehash: 72b1a73bf418b417cd29f88063781e7b45979998
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/09/2020
ms.locfileid: "86105894"
---
# <a name="azure-subscription-as-an-event-grid-source"></a>Azure-abonnement als een Event Grid bron

In dit artikel vindt u de eigenschappen en het schema voor Azure-abonnements gebeurtenissen.Zie [Azure Event grid-gebeurtenis schema](event-schema.md)voor een inleiding tot gebeurtenis schema's.

Azure-abonnementen en-resource groepen verzenden dezelfde gebeurtenis typen. De gebeurtenis typen zijn gerelateerd aan wijzigingen of acties van resources. Het belangrijkste verschil is dat resource groepen gebeurtenissen verzenden voor resources binnen de resource groep en Azure-abonnementen die gebeurtenissen verzenden voor bronnen in het abonnement.

Resource gebeurtenissen worden gemaakt voor PUT-, PATCH-, POST-en DELETE-bewerkingen die worden verzonden naar `management.azure.com` . Bij GET-bewerkingen worden geen gebeurtenissen gemaakt. Bewerkingen die worden verzonden naar het gegevens vlak (zoals `myaccount.blob.core.windows.net` ), maken geen gebeurtenissen. De actie gebeurtenissen bieden gebeurtenis gegevens voor bewerkingen, zoals het weer geven van de sleutels voor een resource.

Wanneer u zich abonneert op gebeurtenissen voor een Azure-abonnement, ontvangt uw eind punt alle gebeurtenissen voor dat abonnement. De gebeurtenissen kunnen gebeurtenissen bevatten die u wilt zien, zoals het bijwerken van een virtuele machine, maar ook gebeurtenissen die mogelijk niet belang rijk voor u zijn, zoals het schrijven van een nieuwe vermelding in de implementatie geschiedenis. U kunt alle gebeurtenissen op uw eind punt ontvangen en code schrijven waarmee de gebeurtenissen worden verwerkt die u wilt verwerken. U kunt ook een filter instellen bij het maken van het gebeurtenis abonnement.

Als u gebeurtenissen op een programmatische manier wilt afhandelen, kunt u gebeurtenissen sorteren door de waarde te bekijken `operationName` . Uw gebeurtenis eindpunt kan bijvoorbeeld alleen gebeurtenissen verwerken voor bewerkingen die gelijk zijn aan `Microsoft.Compute/virtualMachines/write` of `Microsoft.Storage/storageAccounts/write` .

Het gebeurtenis onderwerp is de resource-ID van de resource die het doel van de bewerking is. Als u gebeurtenissen voor een resource wilt filteren, geeft u deze resource-ID op bij het maken van het gebeurtenis abonnement. Als u wilt filteren op een resource type, gebruikt u een waarde in de volgende notatie: `/subscriptions/<subscription-id>/resourcegroups/<resource-group>/providers/Microsoft.Compute/virtualMachines`


## <a name="event-grid-event-schema"></a>Event Grid-gebeurtenisschema

### <a name="available-event-types"></a>Beschik bare gebeurtenis typen

Azure-abonnementen die beheer gebeurtenissen van Azure Resource Manager verzenden, zoals wanneer een virtuele machine wordt gemaakt of een opslag account wordt verwijderd.

| Gebeurtenistype | Beschrijving |
| ---------- | ----------- |
| Micro soft. resources. ResourceActionCancel | Deze gebeurtenis treedt op wanneer de actie voor de resource wordt geannuleerd. |
| Micro soft. resources. ResourceActionFailure | Deze gebeurtenis treedt op wanneer de actie voor de resource mislukt. |
| Micro soft. resources. ResourceActionSuccess | Deze gebeurtenis treedt op wanneer de actie voor de resource slaagt. |
| Micro soft. resources. ResourceDeleteCancel | Deze gebeurtenis treedt op wanneer de verwijderings bewerking is geannuleerd. Deze gebeurtenis treedt op wanneer een sjabloon implementatie wordt geannuleerd. |
| Micro soft. resources. ResourceDeleteFailure | Deze gebeurtenis treedt op wanneer de verwijderings bewerking is mislukt. |
| Micro soft. resources. ResourceDeleteSuccess | Deze gebeurtenis treedt op wanneer delete is voltooid. |
| Micro soft. resources. ResourceWriteCancel | Deze gebeurtenis treedt op wanneer Create-of update-bewerking is geannuleerd. |
| Micro soft. resources. ResourceWriteFailure | Deze gebeurtenis treedt op wanneer Create-of update-bewerking mislukt. |
| Micro soft. resources. ResourceWriteSuccess | Deze gebeurtenis treedt op wanneer Create of update is voltooid. |

### <a name="example-event"></a>Voorbeeld gebeurtenis

In het volgende voor beeld ziet u het schema voor een **ResourceWriteSuccess** -gebeurtenis. Hetzelfde schema wordt gebruikt voor **ResourceWriteFailure** -en **ResourceWriteCancel** -gebeurtenissen met verschillende waarden voor `eventType` .

```json
[{
  "subject": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
  "eventType": "Microsoft.Resources.ResourceWriteSuccess",
  "eventTime": "2018-07-19T18:38:04.6117357Z",
  "id": "4db48cba-50a2-455a-93b4-de41a3b5b7f6",
  "data": {
    "authorization": {
      "scope": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
      "action": "Microsoft.Storage/storageAccounts/write",
      "evidence": {
        "role": "Subscription Admin"
      }
    },
    "claims": {
      "aud": "{audience-claim}",
      "iss": "{issuer-claim}",
      "iat": "{issued-at-claim}",
      "nbf": "{not-before-claim}",
      "exp": "{expiration-claim}",
      "_claim_names": "{\"groups\":\"src1\"}",
      "_claim_sources": "{\"src1\":{\"endpoint\":\"{URI}\"}}",
      "http://schemas.microsoft.com/claims/authnclassreference": "1",
      "aio": "{token}",
      "http://schemas.microsoft.com/claims/authnmethodsreferences": "rsa,mfa",
      "appid": "{ID}",
      "appidacr": "2",
      "http://schemas.microsoft.com/2012/01/devicecontext/claims/identifier": "{ID}",
      "e_exp": "{expiration}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "{last-name}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "{first-name}",
      "ipaddr": "{IP-address}",
      "name": "{full-name}",
      "http://schemas.microsoft.com/identity/claims/objectidentifier": "{ID}",
      "onprem_sid": "{ID}",
      "puid": "{ID}",
      "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "{ID}",
      "http://schemas.microsoft.com/identity/claims/tenantid": "{ID}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": "{user-name}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "{user-name}",
      "uti": "{ID}",
      "ver": "1.0"
    },
    "correlationId": "{ID}",
    "resourceProvider": "Microsoft.Storage",
    "resourceUri": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
    "operationName": "Microsoft.Storage/storageAccounts/write",
    "status": "Succeeded",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}"
  },
  "dataVersion": "2",
  "metadataVersion": "1",
  "topic": "/subscriptions/{subscription-id}"
}]
```

In het volgende voor beeld ziet u het schema voor een **ResourceDeleteSuccess** -gebeurtenis. Hetzelfde schema wordt gebruikt voor **ResourceDeleteFailure** -en **ResourceDeleteCancel** -gebeurtenissen met verschillende waarden voor `eventType` .

```json
[{
  "subject": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
  "eventType": "Microsoft.Resources.ResourceDeleteSuccess",
  "eventTime": "2018-07-19T19:24:12.763881Z",
  "id": "19a69642-1aad-4a96-a5ab-8d05494513ce",
  "data": {
    "authorization": {
      "scope": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
      "action": "Microsoft.Storage/storageAccounts/delete",
      "evidence": {
        "role": "Subscription Admin"
      }
    },
    "claims": {
      "aud": "{audience-claim}",
      "iss": "{issuer-claim}",
      "iat": "{issued-at-claim}",
      "nbf": "{not-before-claim}",
      "exp": "{expiration-claim}",
      "_claim_names": "{\"groups\":\"src1\"}",
      "_claim_sources": "{\"src1\":{\"endpoint\":\"{URI}\"}}",
      "http://schemas.microsoft.com/claims/authnclassreference": "1",
      "aio": "{token}",
      "http://schemas.microsoft.com/claims/authnmethodsreferences": "rsa,mfa",
      "appid": "{ID}",
      "appidacr": "2",
      "http://schemas.microsoft.com/2012/01/devicecontext/claims/identifier": "{ID}",
      "e_exp": "262800",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "{last-name}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "{first-name}",
      "ipaddr": "{IP-address}",
      "name": "{full-name}",
      "http://schemas.microsoft.com/identity/claims/objectidentifier": "{ID}",
      "onprem_sid": "{ID}",
      "puid": "{ID}",
      "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "{ID}",
      "http://schemas.microsoft.com/identity/claims/tenantid": "{ID}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": "{user-name}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "{user-name}",
      "uti": "{ID}",
      "ver": "1.0"
    },
    "correlationId": "{ID}",
    "httpRequest": {
      "clientRequestId": "{ID}",
      "clientIpAddress": "{IP-address}",
      "method": "DELETE",
      "url": "https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2018-02-01"
    },
    "resourceProvider": "Microsoft.Storage",
    "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
    "operationName": "Microsoft.Storage/storageAccounts/delete",
    "status": "Succeeded",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}"
  },
  "dataVersion": "2",
  "metadataVersion": "1",
  "topic": "/subscriptions/{subscription-id}"
}]
```

In het volgende voor beeld ziet u het schema voor een **ResourceActionSuccess** -gebeurtenis. Hetzelfde schema wordt gebruikt voor **ResourceActionFailure** -en **ResourceActionCancel** -gebeurtenissen met verschillende waarden voor `eventType` .

```json
[{   
  "subject": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{namespace}/AuthorizationRules/RootManageSharedAccessKey",
  "eventType": "Microsoft.Resources.ResourceActionSuccess",
  "eventTime": "2018-10-08T22:46:22.6022559Z",
  "id": "{ID}",
  "data": {
    "authorization": {
      "scope": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{namespace}/AuthorizationRules/RootManageSharedAccessKey",
      "action": "Microsoft.EventHub/namespaces/AuthorizationRules/listKeys/action",
      "evidence": {
        "role": "Contributor",
        "roleAssignmentScope": "/subscriptions/{subscription-id}",
        "roleAssignmentId": "{ID}",
        "roleDefinitionId": "{ID}",
        "principalId": "{ID}",
        "principalType": "ServicePrincipal"
      }     
    },
    "claims": {
      "aud": "{audience-claim}",
      "iss": "{issuer-claim}",
      "iat": "{issued-at-claim}",
      "nbf": "{not-before-claim}",
      "exp": "{expiration-claim}",
      "aio": "{token}",
      "appid": "{ID}",
      "appidacr": "2",
      "http://schemas.microsoft.com/identity/claims/identityprovider": "{URL}",
      "http://schemas.microsoft.com/identity/claims/objectidentifier": "{ID}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "{ID}",       "http://schemas.microsoft.com/identity/claims/tenantid": "{ID}",
      "uti": "{ID}",
      "ver": "1.0"
    },
    "correlationId": "{ID}",
    "httpRequest": {
      "clientRequestId": "{ID}",
      "clientIpAddress": "{IP-address}",
      "method": "POST",
      "url": "https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{namespace}/AuthorizationRules/RootManageSharedAccessKey/listKeys?api-version=2017-04-01"
    },
    "resourceProvider": "Microsoft.EventHub",
    "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{namespace}/AuthorizationRules/RootManageSharedAccessKey",
    "operationName": "Microsoft.EventHub/namespaces/AuthorizationRules/listKeys/action",
    "status": "Succeeded",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}"
  },
  "dataVersion": "2",
  "metadataVersion": "1",
  "topic": "/subscriptions/{subscription-id}" 
}]
```

### <a name="event-properties"></a>Gebeurtenis eigenschappen

Een gebeurtenis heeft de volgende gegevens op het hoogste niveau:

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| onderwerp | tekenreeks | Volledige bronpad naar de bron van de gebeurtenis. Dit veld is niet beschrijfbaar. Event Grid biedt deze waarde. |
| onderwerp | tekenreeks | Het door de uitgever gedefinieerde pad naar het gebeurtenisonderwerp. |
| Type | tekenreeks | Een van de geregistreerde gebeurtenistypen voor deze gebeurtenisbron. |
| eventTime | tekenreeks | Het tijdstip waarop de gebeurtenis is gegenereerd op basis van de UTC-tijd van de provider. |
| id | tekenreeks | De unieke id voor de gebeurtenis. |
| gegevens | object | Gebeurtenis gegevens van abonnement. |
| dataVersion | tekenreeks | De schemaversie van het gegevensobject. De uitgever definieert de schemaversie. |
| metadataVersion | tekenreeks | De schemaversie van de metagegevens van de gebeurtenis. Event Grid definieert het schema voor de eigenschappen op het hoogste niveau. Event Grid biedt deze waarde. |

Het gegevens object heeft de volgende eigenschappen:

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| autorisatie | object | De aangevraagde autorisatie voor de bewerking. |
| claims | object | De eigenschappen van de claims. Zie [JWT-specificatie](https://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)voor meer informatie. |
| correlationId | tekenreeks | Een bewerkings-ID voor het oplossen van problemen. |
| httpRequest | object | De details van de bewerking. Dit object is alleen opgenomen bij het bijwerken van een bestaande resource of het verwijderen van een resource. |
| Resource provider | tekenreeks | De resource provider voor de bewerking. |
| resourceUri | tekenreeks | De URI van de resource in de bewerking. |
| operationName | tekenreeks | De bewerking die is uitgevoerd. |
| status | tekenreeks | De status van de bewerking. |
| subscriptionId | tekenreeks | De abonnements-ID van de resource. |
| tenantId | tekenreeks | De Tenant-ID van de resource. |

## <a name="tutorials-and-how-tos"></a>Zelfstudies en handleidingen
|Titel |Beschrijving  |
|---------|---------|
| [Zelf studie: Azure Automation met Event Grid en micro soft teams](ensure-tags-exists-on-new-virtual-machines.md) |Maak een virtuele machine die een gebeurtenis verzendt. De gebeurtenis activeert een Automation-runbook waarmee de virtuele machine wordt gecodeerd en een bericht wordt geactiveerd dat naar een micro soft teams-kanaal wordt verzonden. |
| [Procedure: abonneren op gebeurtenissen via de portal](subscribe-through-portal.md) | Gebruik de portal om u te abonneren op gebeurtenissen voor een Azure-abonnement. |
| [Azure CLI: abonneren op gebeurtenissen voor een Azure-abonnement](./scripts/event-grid-cli-azure-subscription.md) |Voorbeeld script voor het maken van een Event Grid-abonnement op een Azure-abonnement en het verzenden van gebeurtenissen naar een webhook. |
| [Power shell: abonneren op gebeurtenissen voor een Azure-abonnement](./scripts/event-grid-powershell-azure-subscription.md)| Voorbeeld script voor het maken van een Event Grid-abonnement op een Azure-abonnement en het verzenden van gebeurtenissen naar een webhook. |

## <a name="next-steps"></a>Volgende stappen

* Zie [Wat is Event grid?](overview.md)voor een inleiding tot Azure Event grid.
* Zie [Event grid Subscription schema](subscription-creation-schema.md)voor meer informatie over het maken van een Azure Event grid-abonnement.
