---
title: 'Zelfstudie: Verificatie toevoegen aan een web-app in Azure App Service | Azure'
description: In deze zelfstudie leert u hoe u verificatie en autorisatie inschakelt voor een web-app die wordt uitgevoerd in Azure App Service.  Beperk de toegang tot de web-app tot gebruikers in mijn organisatie.
services: active-directory, app-service-web
author: rwike77
manager: CelesteDG
ms.service: app-service-web
ms.topic: tutorial
ms.workload: identity
ms.date: 11/09/2020
ms.author: ryanwi
ms.reviewer: stsoneff
ms.openlocfilehash: a1b2809371a01b1c6fd822e5c4aaa197d0de3c1b
ms.sourcegitcommit: 0dcafc8436a0fe3ba12cb82384d6b69c9a6b9536
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/10/2020
ms.locfileid: "94428205"
---
# <a name="tutorial-add-authentication-to-your-web-app-running-on-azure-app-service"></a>Zelfstudie: Verificatie toevoegen aan uw web-app die wordt uitgevoerd in Azure App Service

Ontdek hoe u verificatie inschakelt voor uw web-app die wordt uitgevoerd in Azure App Service, en de toegang beperkt tot gebruikers in uw organisatie.

:::image type="content" source="./media/scenario-secure-app-authentication-app-service/web-app-sign-in.svg" alt-text="Gebruiker aanmelden" border="false":::

Azure App Service biedt ingebouwde ondersteuning voor verificatie en autorisatie, zodat u gebruikers kunt aanmelden en toegang tot gegevens kunt krijgen door minimale of helemaal geen code te schrijven in uw web-app.  Het is niet verplicht de module App Service-verificatie/-autorisatie te gebruiken, maar het helpt wel de verificatie en autorisatie voor uw app te vereenvoudigen. In dit artikel wordt uitgelegd hoe u uw web-app beveiligt met de module App Service-verificatie/-autorisatie door Azure Active Directory als de id-provider te gebruiken.

De verificatie-/autorisatiemodule wordt ingeschakeld en geconfigureerd via de Azure-portal en app-instellingen. Er zijn geen SDK's, specifieke talen of wijzigingen in de toepassingscode nodig. Er worden verschillende id-providers ondersteund, waaronder: Azure AD, Microsoft Account, Facebook, Google en Twitter. Wanneer de verificatie-/autorisatiemodule is ingeschakeld, gaat elke inkomende HTTP-aanvraag via de module voordat de aanvraag wordt verwerkt door app-code.  Lees [Verificatie en autorisatie in Azure App Service](overview-authentication-authorization.md) voor meer informatie.

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
>
> * Verificatie configureren voor de web-app
> * De toegang tot de web-app beperken tot gebruikers in uw organisatie

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-and-publish-a-web-app-on-app-service"></a>Een web-app maken en publiceren in App Service

Voor deze zelfstudie moet er een web-app zijn geïmplementeerd in Azure App Service.  U kunt een bestaande web-app gebruiken of u kunt de [snelstartgids voor ASP.NET Core](quickstart-dotnetcore.md) volgen om een nieuwe web-app te maken en publiceren in App Service.

Of u nu een bestaande web-app gebruikt of een nieuwe maakt, noteer de naam van de web-app en de naam van de resourcegroep waarin de web-app is geïmplementeerd. U hebt deze namen nodig in deze zelfstudie. In deze zelfstudie bevatten voorbeeldnamen in procedures en schermafbeeldingen de naam *SecureWebApp*.

## <a name="configure-authentication-and-authorization"></a>Verificatie en autorisatie configureren

U hebt nu een web-app die wordt uitgevoerd in App Service.  Vervolgens schakelt u verificatie en autorisatie voor de web-app in. U gebruikt Azure Active Directory als id-provider. Zie [Verificatie van Azure Active Directory configureren voor de App Services-toepassing](configure-authentication-provider-aad.md) voor meer informatie.

Selecteer in het menu van de [Azure-portal](https://portal.azure.com) de optie **Resourcegroepen** of zoek ernaar en selecteer *Resourcegroepen* vanaf een willekeurige pagina.

Zoek in **Resourcegroepen** uw resourcegroep en selecteer deze. Selecteer in **Overzicht** de beheerpagina van uw app.

:::image type="content" alt-text="App Service selecteren" source="./media/scenario-secure-app-authentication-app-service/select-app-service.png":::

Selecteer in het linkermenu van uw app de optie **Verificatie/autorisatie** en schakel vervolgens App Service-verificatie in door **Aan** te selecteren.

Selecteer **Te ondernemen actie wanneer de aanvraag niet is geverifieerd** de optie **Aanmelden met Azure Active Directory**.

Selecteer onder **Azure Active Directory** de optie **Verificatieproviders**. Selecteer **Express** en accepteer vervolgens de standaardinstellingen om een nieuwe AD-app te maken. Selecteer vervolgens **OK**.

:::image type="content" alt-text="Express-verificatie" source="./media/scenario-secure-app-authentication-app-service/configure-authentication.png":::

Selecteer op de pagina **Verificatie/autorisatie** de optie **Opslaan**.

Vernieuw de portalpagina als de melding met het bericht `Successfully saved the Auth Settings for <app-name> App` wordt weergegeven.

U hebt nu een app die wordt beveiligd door App Service-verificatie en -autorisatie.

## <a name="verify-limited-access-to-the-web-app"></a>Beperkte toegang tot de web-app verifiëren

Toen u de module App Service-verificatie/-autorisatie inschakelde, werd er een app-registratie gemaakt in uw Azure AD-tenant.  De app-registratie heeft dezelfde weergavenaam als uw web-app. Om de instellingen te controleren, selecteert u **Azure Active Directory** in het portalmenu en selecteert u vervolgens **App-registraties**.  Selecteer de app-registratie die is gemaakt.  Verifieer in het overzicht dat **Ondersteunde accounttypen** is ingesteld op **Alleen mijn organisatie**.

:::image type="content" alt-text="Toegang verifiëren" source="./media/scenario-secure-app-authentication-app-service/verify-access.png":::

Om te verifiëren dat de toegang tot uw app is beperkt tot gebruikers in uw organisatie, start u een browser in incognito- of privémodus en gaat u naar `https://<app-name>.azurewebsites.net`.  U wordt naar een beveiligde aanmeldingspagina geleid, wat verifieert dat niet-geverifieerde gebruikers geen toegang tot de site hebben.  Meld u aan als gebruiker in uw organisatie om toegang tot de site te krijgen.  U kunt ook een nieuwe browser starten en zich proberen aan te melden met een persoonlijk account om te verifiëren dat gebruikers buiten de organisatie geen toegang hebben.  

## <a name="clean-up-resources"></a>Resources opschonen

Als u klaar bent met deze zelfstudie en de web-app of bijbehorende resources niet meer nodig hebt, kunt u [de gemaakte resources opschonen](scenario-secure-app-clean-up-resources.md).

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]
>
> * Verificatie configureren voor de web-app
> * De toegang tot de web-app beperken tot gebruikers in uw organisatie

> [!div class="nextstepaction"]
> [App Service krijgt toegang tot opslag](scenario-secure-app-access-storage.md)
