---
title: Anomaly Detector-omgevingsvariabelen
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: mrbullwinkle
manager: nitinme
ms.service: cognitive-services
ms.topic: include
ms.date: 06/30/2020
ms.author: mbullwin
ms.openlocfilehash: 5148114da7fcc654b1f0af431440ce74c7bc8d31
ms.sourcegitcommit: 22da82c32accf97a82919bf50b9901668dc55c97
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/08/2020
ms.locfileid: "94371764"
---
### <a name="create-an-environment-variable"></a>Een omgevingsvariabele maken

>[!NOTE]
> De eindpunten voor niet-proefversie-resources die zijn gemaakt na 1 juli 2019, gebruiken de aangepaste indeling voor subdomeinen die hieronder wordt weergegeven. Zie [Aangepaste subdomeinnamen voor Cognitive Services](../../cognitive-services-custom-subdomains.md) voor meer informatie en een volledige lijst met regionale eindpunten. 

Maak met uw sleutel en eindpunt van de resource die u hebt gemaakt, twee omgevingsvariabelen voor verificatie:

* `ANOMALY_DETECTOR_KEY`: de resourcesleutel voor het verifiëren van uw aanvragen.
* `ANOMALY_DETECTOR_ENDPOINT`: het resource-eindpunt voor het verzenden van API-aanvragen. Dit ziet er als volgt uit: 
  * `https://<your-custom-subdomain>.api.cognitive.microsoft.com` 

Volg de instructies voor uw besturingssysteem.

#### <a name="windows"></a>[Windows](#tab/windows)

```console
setx ANOMALY_DETECTOR_KEY <replace-with-your-anomaly-detector-key>
setx ANOMALY_DETECTOR_ENDPOINT <replace-with-your-anomaly-detector-endpoint>
```

Nadat u de omgevingsvariabele hebt toegevoegd, start u het consolevenster opnieuw.

#### <a name="linux"></a>[Linux](#tab/linux)

```bash
export ANOMALY_DETECTOR_KEY=<replace-with-your-anomaly-detector-key>
export ANOMALY_DETECTOR_ENDPOINT=<replace-with-your-anomaly-detector-endpoint>
```

Nadat u de omgevingsvariabele toevoegt, voert u `source ~/.bashrc` uit vanuit het consolevenster om de wijzigingen van kracht te laten worden.

#### <a name="macos"></a>[MacOS](#tab/unix)

Bewerk uw `.bash_profile` en voeg de omgevingsvariabele toe:

```bash
export ANOMALY_DETECTOR_KEY=<replace-with-your-anomaly-detector-key>
export ANOMALY_DETECTOR_ENDPOINT=<replace-with-your-anomaly-detector-endpoint>
```

Nadat u de omgevingsvariabele toevoegt, voert u `source .bash_profile` uit vanuit het consolevenster om de wijzigingen van kracht te laten worden.

***