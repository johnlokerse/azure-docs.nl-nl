---
title: Een functie-app met verbonden opslag maken - Azure CLI
description: Azure CLI-scriptvoorbeeld - Een Azure-functie maken die verbinding maakt met een Azure Storage
ms.topic: sample
ms.date: 04/20/2017
ms.custom: mvc, devx-track-azurecli
ms.openlocfilehash: 3eec4e22f80d1efd180dc6770a781ee14db680be
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/09/2020
ms.locfileid: "87498545"
---
# <a name="create-a-function-app-with-a-named-storage-account-connection"></a>Een functie-app maken met een benoemde verbinding voor een opslagaccount 

Met dit Azure Functions-voorbeeldscript wordt een functie-app gemaakt en wordt de functie verbonden met een Azure Storage-account. De gemaakte app-instelling die de verbinding bevat, kan worden gebruikt met een [opslagtrigger of -binding](../functions-bindings-storage-blob.md). 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u de CLI lokaal gebruikt, moet u ervoor zorgen dat u Azure CLI versie 2.0 of hoger gebruikt. Voer `az --version` uit om de versie te bekijken. Als u uw CLI wilt installeren of upgraden, raadpleegt u [De Azure CLI installeren](/cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeldscript

In dit voorbeeld wordt een Azure-functie-app gemaakt en wordt de opslagverbindingsreeks toegevoegd aan een app-instelling.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Uitleg van het script

In dit script worden de volgende opdrachten gebruikt. Elke opdracht in de tabel is een koppeling naar specifieke documentatie over de opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [az group create](/cli/azure/group#az-group-create) | Hiermee maakt u een resourcegroep met locatie. |
| [az storage account create](/cli/azure/storage/account#az-storage-account-create) | Een opslagaccount maken. |
| [az functionapp create](/cli/azure/functionapp#az-functionapp-create) | Hiermee maakt u een functie-app in het serverloze [verbruiksabonnement](../functions-scale.md#consumption-plan). |
| [az storage account show-connection-string](/cli/azure/storage/account#az-storage-account-show-connection-string) | Hiermee wordt de verbindingsreeks voor het account opgehaald. |
| [az functionapp config appsettings set](/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-set) | Hiermee stelt u de verbindingsreeks in als een app-instelling in de functie-app. |

## <a name="next-steps"></a>Volgende stappen

Raadpleeg de [documentatie van Azure CLI](/cli/azure) voor meer informatie over de Azure CLI.

Aanvullende CLI-voorbeeldscripts voor Azure Functions vindt u in de [Azure Functions-documentatie](../functions-cli-samples.md).
