---
author: trevorbye
ms.service: cognitive-services
ms.topic: include
ms.date: 03/20/2020
ms.author: trbye
ms.openlocfilehash: 9365b4bbf6e6fb37156b6e9f24b923591945ea52
ms.sourcegitcommit: d95cab0514dd0956c13b9d64d98fdae2bc3569a0
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/25/2020
ms.locfileid: "91376403"
---
## <a name="prerequisites"></a>Vereisten

Voordat u aan de slag gaat, moet u het volgende doen:

> [!div class="checklist"]
> * [Een resource voor de Azure-spraakservice maken](../../../../overview.md#try-the-speech-service-for-free)
> * [Een LUIS-toepassing maken en een eindpuntsleutel verkrijgen](../../../../quickstarts/create-luis.md)
> * [Uw ontwikkelomgeving instellen en een leeg project maken](../../../../quickstarts/setup-platform.md?pivots=programming-language-python)

[!INCLUDE [Audio input format](~/articles/cognitive-services/speech-service/includes/audio-input-format-chart.md)]

## <a name="support-and-updates"></a>Ondersteuning en updates

Updates voor het Python Speech-SDK-pakket worden gedistribueerd via PyPI en aangekondigd in de [Releaseopmerkingen](~/articles/cognitive-services/Speech-Service/releasenotes.md).
Als een nieuwe versie beschikbaar is, kunt u een update naar deze versie uitvoeren met behulp van de opdracht `pip install --upgrade azure-cognitiveservices-speech`.
U kunt controleren welke versie momenteel is geïnstalleerd door de variabele `azure.cognitiveservices.speech.__version__` te bekijken.

Zie [opties voor ondersteuning en hulp](~/articles/cognitive-services/Speech-Service/support.md) als er een probleem is of als er een functie ontbreekt.

## <a name="create-a-python-application-that-uses-the-speech-sdk"></a>Een Python-toepassing maken dat de Speech-SDK gebruikt

### <a name="run-the-sample"></a>De voorbeeldtoepassing uitvoeren

U kunt de [voorbeeldcode](#sample-code) uit deze quickstart kopiëren naar een `quickstart.py`-bronbestand en de voorbeeldcode uitvoeren in uw IDE of in de console:

```Bash
python quickstart.py
```

Of u kunt deze quickstart-zelfstudie downloaden als een [Jupyter](https://jupyter.org)-notebook uit de [opslagplaats met Speech-SDK-voorbeelden](https://github.com/Azure-Samples/cognitive-services-speech-sdk/) en de quickstart uitvoeren als een notitieblok.

### <a name="sample-code"></a>Voorbeeldcode

> [!NOTE]
> De Speech-SDK probeert taal standaard te herkennen in en-US. Zie [De brontaal voor spraak-naar-tekst opgeven](../../../../how-to-specify-source-language.md) voor informatie over het kiezen van de brontaal.

```python
import azure.cognitiveservices.speech as speechsdk

# Creates an instance of a speech config with specified subscription key and service region.
# Replace with your own subscription key and region identifier from here: https://aka.ms/speech/sdkregion
speech_key, service_region = "YourSubscriptionKey", "YourServiceRegion"
speech_config = speechsdk.SpeechConfig(subscription=speech_key, region=service_region)

# Creates an audio configuration that points to an audio file.
# Replace with your own audio filename.
audio_filename = "whatstheweatherlike.wav"
audio_input = speechsdk.audio.AudioConfig(filename=audio_filename)

# Creates a recognizer with the given settings
speech_recognizer = speechsdk.SpeechRecognizer(speech_config=speech_config, audio_config=audio_input)

print("Recognizing first result...")

# Starts speech recognition, and returns after a single utterance is recognized. The end of a
# single utterance is determined by listening for silence at the end or until a maximum of 15
# seconds of audio is processed.  The task returns the recognition text as result. 
# Note: Since recognize_once() returns only a single utterance, it is suitable only for single
# shot recognition like command or query. 
# For long-running multi-utterance recognition, use start_continuous_recognition() instead.
result = speech_recognizer.recognize_once()

# Checks result.
if result.reason == speechsdk.ResultReason.RecognizedSpeech:
    print("Recognized: {}".format(result.text))
elif result.reason == speechsdk.ResultReason.NoMatch:
    print("No speech could be recognized: {}".format(result.no_match_details))
elif result.reason == speechsdk.ResultReason.Canceled:
    cancellation_details = result.cancellation_details
    print("Speech Recognition canceled: {}".format(cancellation_details.reason))
    if cancellation_details.reason == speechsdk.CancellationReason.Error:
        print("Error details: {}".format(cancellation_details.error_details))
```

### <a name="install-and-use-the-speech-sdk-with-visual-studio-code"></a>De Speech-SDK installeren en gebruiken met Visual Studio Code

1. Download en installeer een 64-bits versie (3.5 tot 3.8) van [Python](https://www.python.org/downloads/) op de computer.
1. Download en installeer [Visual Studio Code](https://code.visualstudio.com/Download).
1. Open Visual Studio Code en installeer de Python-extensie. Selecteer **Bestand** > **Voorkeuren** > **Extensies** in het menu. Zoek naar **Python**.

   ![De Python-extensie installeren](~/articles/cognitive-services/Speech-Service/media/sdk/qs-python-vscode-python-extension.png)

1. Maak een map om daar het project in op te slaan. Dat kunt u bijvoorbeeld doen met Windows Verkenner.
1. Selecteer in Visual Studio Code het pictogram **Bestand**. Open vervolgens de map die u hebt gemaakt.

   ![Een map openen](~/articles/cognitive-services/Speech-Service/media/sdk/qs-python-vscode-python-open-folder.png)

1. Maak een nieuw Python-bronbestand, `speechsdk.py`, door het pictogram Nieuw bestand te selecteren.

   ![Een bestand maken](~/articles/cognitive-services/Speech-Service/media/sdk/qs-python-vscode-python-newfile.png)

1. Kopieer en plak de [Python-code](#sample-code) en sla deze op in het zojuist gemaakte bestand.
1. Voeg de gegevens van uw Speech Service-abonnement in.
1. Als er een Python-interpreter is geselecteerd, wordt deze onder aan het venster weergegeven, links van de statusbalk.
   Anders wordt er een lijst met beschikbare Python-interpreters geopend. Open het opdrachtenpalet <kbd>Ctrl+Shift+P</kbd> en voer **Python: Interpreter selecteren** in. Kies de juiste versie.
1. U kunt het Python Speech-SDK-pakket installeren vanuit Visual Studio Code. Doe dat als het pakket nog niet is geïnstalleerd voor de Python-interpreter die u hebt geselecteerd.
   Open een terminal voor het installeren van het Speech-SDK-pakket. Open het opdrachtenpalet opnieuw <kbd>Ctrl+Shift+P</kbd> en voer **Terminal: Nieuwe geïntegreerde terminal maken**.
   Voer in de terminal die wordt geopend, de opdracht `python -m pip install azure-cognitiveservices-speech` in, of de juiste opdracht voor uw systeem.
1. Als u de voorbeeldcode wilt uitvoeren, klikt u met de rechtermuisknop ergens in de editor. Selecteer **Python-bestand uitvoeren in de Terminal**.
   De eerste 15 seconden aan spraakinvoer vanuit uw geluidsbestand worden herkend en geregistreerd in het consolevenster.

   ```console
   Recognizing first result...
   We recognized: What's the weather like?
   ```

Als er zich problemen voordoen met deze instructies, raadpleegt u de uitgebreidere [Python-zelfstudie voor Visual Studio Code](https://code.visualstudio.com/docs/python/python-tutorial).

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [Speech recognition basics](../../speech-to-text-next-steps.md)]