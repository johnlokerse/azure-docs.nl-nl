---
title: Een PowerShell-functie maken met behulp van Visual Studio Code - Azure Functions
description: Leer hoe u een PowerShell-functie maakt en publiceer vervolgens het lokale project naar serverloze hosting in Azure Functions met behulp van de Azure Functions-extensie in Visual Studio Code.
ms.topic: quickstart
ms.date: 11/04/2020
ms.openlocfilehash: 73c2de36d3696356289c72d08c29c3870dc91601
ms.sourcegitcommit: 0dcafc8436a0fe3ba12cb82384d6b69c9a6b9536
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/10/2020
ms.locfileid: "94427391"
---
# <a name="quickstart-create-a-powershell-function-in-azure-using-visual-studio-code"></a>Quickstart: Een PowerShell-functie maken in Azure met behulp van Visual Studio Code

[!INCLUDE [functions-language-selector-quickstart-vs-code](../../includes/functions-language-selector-quickstart-vs-code.md)]

In dit artikel gebruikt u Visual Studio Code om een PowerShell-functie te maken die reageert op HTTP-aanvragen. Nadat u de code lokaal hebt getest, implementeert u deze in de serverloze omgeving van Azure Functions.

Voor het voltooien van deze quickstart worden kosten van een paar dollarcent of minder in rekening gebracht bij uw Azure-account.

Er is ook een [op een CLI gebaseerde versie](create-first-function-cli-powershell.md) van dit artikel.

## <a name="configure-your-environment"></a>Uw omgeving configureren

Voordat u aan de slag kunt gaan, moet u beschikken over de volgende vereisten:

+ Een Azure-account met een actief abonnement. [Gratis een account maken](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)

+ [Node.js](https://nodejs.org/), vereist door Windows voor NPM. Alleen [Active LTS en Maintenance LTS-versies](https://nodejs.org/about/releases/). Gebruik de opdracht `node --version` om uw versie te controleren.
    Niet vereist voor lokale ontwikkeling in macOS en Linux.

+ [PowerShell 7](/powershell/scripting/install/installing-powershell-core-on-windows)

+ Zowel [.NET Core 3.1](https://www.microsoft.com/net/download) als [.NET Core 2.1](https://dotnet.microsoft.com/download/dotnet-core/2.1)  

+ [Visual Studio Code](https://code.visualstudio.com/) op een van de [ondersteunde platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).    

+ De [PowerShell-extensie voor Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell).  

+ De [Azure Functions-extensie](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) voor Visual Studio Code. 

## <a name="create-your-local-project"></a><a name="create-an-azure-functions-project"></a>Uw lokale project maken

In deze sectie gebruikt u Visual Studio Code om een lokaal Azure Functions-project te maken in PowerShell. Verderop in dit artikel publiceert u de functiecode in Azure.

1. Kies het Azure-pictogram in de activiteitenbalk en selecteer vervolgens in het gedeelte **Azure: Functions** het pictogram **Nieuw project maken...** .

    ![Een nieuw project maken kiezen](./media/functions-create-first-function-vs-code/create-new-project.png)

1. Kies een maplocatie voor de werkruimte van uw project en kies **Selecteren**.

    > [!NOTE]
    > Deze stappen waren bedoeld om buiten een werkruimte te worden voltooid. Selecteer in dit geval geen projectmap die deel uitmaakt van een werkruimte.

1. Geef de volgende informatie op bij de prompts:

    + **Selecteer een taal voor uw functieproject**: Kies `PowerShell`.

    + **Selecteer een sjabloon voor de eerste functie van uw project**: Kies `HTTP trigger`.

    + **Geef een functienaam op**: Typ `HttpExample`.

    + **Autorisatieniveau**: Kies `Anonymous`, waarmee iedereen uw functie-eindpunt kan aanroepen. Zie [Autorisatiesleutels](functions-bindings-http-webhook-trigger.md#authorization-keys) voor meer informatie over autorisatieniveau.

    + **Selecteer hoe u uw project wilt openen**: Kies `Add to workspace`.

1. Met behulp van deze informatie wordt met Visual Studio Code een Azure Functions-project gegenereerd met een HTTP-trigger. U kunt de lokale projectbestanden weergeven in de Explorer. Zie [Gegenereerde projectbestanden](functions-develop-vs-code.md#generated-project-files) voor meer informatie over bestanden die worden gemaakt. 

[!INCLUDE [functions-run-function-test-local-vs-code-ps](../../includes/functions-run-function-test-local-vs-code-ps.md)]

Nadat u hebt gecontroleerd of de functie correct wordt uitgevoerd op uw lokale computer, is het tijd om het project te publiceren in Azure met behulp van Visual Studio Code. 

[!INCLUDE [functions-sign-in-vs-code](../../includes/functions-sign-in-vs-code.md)]

[!INCLUDE [functions-publish-project-vscode](../../includes/functions-publish-project-vscode.md)]

[!INCLUDE [functions-vs-code-run-remote](../../includes/functions-vs-code-run-remote.md)]

[!INCLUDE [functions-cleanup-resources-vs-code.md](../../includes/functions-cleanup-resources-vs-code.md)]

## <a name="next-steps"></a>Volgende stappen

U hebt een functie-app met een eenvoudige HTTP-geactiveerde functie gemaakt in Visual Studio Code. In het volgende artikel vouwt u die functie uit door een uitvoerbinding toe te voegen. Met deze binding wordt de tekenreeks van de HTTP-aanvraag naar een bericht in een Azure Queue Storage-wachtrij geschreven. 

> [!div class="nextstepaction"]
> [Verbinding maken met een Azure Storage-wachtrij](functions-add-output-binding-storage-queue-vs-code.md?pivots=programming-language-powershell)

[Azure Functions Core Tools]: functions-run-local.md
[Azure Functions extension for Visual Studio Code]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions
