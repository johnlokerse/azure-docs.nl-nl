---
author: nikuklic
ms.service: azure-communication-services
ms.topic: include
ms.date: 9/11/2020
ms.author: nikuklic
ms.openlocfilehash: 63fd0af819fde7d78df289a1b8f5cefa2e415101
ms.sourcegitcommit: d9ba60f15aa6eafc3c5ae8d592bacaf21d97a871
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2020
ms.locfileid: "91779177"
---
[!INCLUDE [Emergency Calling Notice](../../../includes/emergency-calling-notice-include.md)]
## <a name="prerequisites"></a>Vereisten

- Een Azure-account met een actief abonnement. [Gratis een account maken](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 
- Een geïmplementeerde Communication Services-resource. [Een Communication Services maken](../../create-communication-resource.md).
- Een telefoonnummer dat is verkregen in de Communication Services-resource. [Een telefoonnummer aanvragen](../../telephony-sms/get-phone-number.md).
- Een `User Access Token` om de aanroepende client in te schakelen. Voor meer informatie over het [verkrijgen van een `User Access Token`](../../access-tokens.md)
- Voltooi de quickstart om [aan de slag te gaan met het toevoegen van aanroepen aan uw toepassing](../getting-started-with-calling.md)

### <a name="prerequisite-check"></a>Controle van vereisten

- Als u de telefoonnummers wilt weergeven die zijn gekoppeld aan uw Communication Services-resource, meldt u zich aan bij [Azure Portal](https://portal.azure.com/), zoekt u uw Communication Services-resource en opent u het tabblad **telefoonnummers** vanuit het navigatiedeelvenster aan de linkerkant.
- U kunt uw app bouwen en uitvoeren met de clientbibliotheek voor oproepen voor iOS in Azure Communication Services:

## <a name="setting-up"></a>Instellen

## <a name="start-a-call-to-phone"></a>Een telefoongesprek starten

Geef het telefoonnummer op dat u hebt verkregen in de Communication Services-resource die wordt gebruikt om het gesprek te starten:
> [!WARNING]
> Houd er rekening mee dat telefoonnummers moeten worden opgegeven in de internationale standaardindeling E.164. (bijvoorbeeld: +12223334444)

Wijzig de gebeurtenis-handler `startCall` die wordt uitgevoerd wanneer op de knop *Oproep starten* wordt getikt:

```swift
func startCall() {
    // Ask permissions
    AVAudioSession.sharedInstance().requestRecordPermission { (granted) in
        if granted {
            let startCallOptions = ACSStartCallOptions()
            startCallOptions!.alternateCallerID = PhoneNumber(phoneNumber: "+12223334444")
            self.call = self.callAgent!.call([PhoneNumber(phoneNumber: self.callee)], options: startCallOptions)
            self.callDelegate = CallDelegate(self)
            self.call!.delegate = self.callDelegate
        }
    }
}
```

## <a name="run-the-code"></a>De code uitvoeren

U kunt uw app maken en uitvoeren op een iOS-simulator door **Product** > **Uitvoeren** te selecteren of door de sneltoets (&#8984;-R) te gebruiken.

![Laatste look en feel van de snelstart-app](../media/ios/quick-start-make-call.png)

U kunt een oproep naar een telefoonnummer plaatsen door een telefoonnummer op te geven in het toegevoegde tekstveld en te klikken op de knop **Oproep starten**.
> [!WARNING]
> Houd er rekening mee dat telefoonnummers moeten worden opgegeven in de internationale standaardindeling E.164. (bijvoorbeeld: +12223334444)

> [!NOTE]
> De eerste keer dat u een oproep doet, wordt u gevraagd om toegang tot de microfoon. In een productietoepassing moet u de `AVAudioSession`API[ gebruiken om de machtigingsstatus](https://developer.apple.com/documentation/uikit/protecting_the_user_s_privacy/requesting_access_to_protected_resources) te controleren en het gedrag van uw toepassing bij te werken wanneer geen toestemming wordt verleend.
