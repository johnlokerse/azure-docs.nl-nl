---
title: Pijplijn uitvoeringen bewaken met behulp van Synapse Studio
description: Gebruik de Synapse Studio om uw werk ruimte pijplijn uitvoeringen te bewaken.
services: synapse-analytics
author: matt1883
ms.service: synapse-analytics
ms.topic: how-to
ms.subservice: monitoring
ms.date: 10/27/2020
ms.author: mahi
ms.reviewer: mahi
ms.openlocfilehash: 61d860def7209908e65e9456a4bcde87eed522fc
ms.sourcegitcommit: 8c7f47cc301ca07e7901d95b5fb81f08e6577550
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/27/2020
ms.locfileid: "92746383"
---
# <a name="use-synapse-studio-to-monitor-your-workspace-pipeline-runs"></a>Synapse Studio gebruiken om de pipeline-uitvoeringen van uw werk ruimte te controleren

Met Azure Synapse Analytics kunt u complexe pijp lijnen maken die uw gegevens verplaatsing, gegevens transformatie en reken activiteiten binnen uw oplossing kunnen automatiseren en integreren. U kunt deze pijp lijnen ontwerpen en bewaken met behulp van Synapse Studio (preview).

In dit artikel wordt uitgelegd hoe u uw pijplijn uitvoeringen kunt bewaken, zodat u op de hoogte blijft van de meest recente status, problemen en voortgang van uw pijp lijnen.

## <a name="access-pipeline-runs-list"></a>Lijst met open pipeline-uitvoeringen

Als u de lijst met pijplijn uitvoeringen in uw werk ruimte wilt zien, opent u eerst [de Synapse Studio](https://web.azuresynapse.net/) en selecteert u uw werk ruimte.

![Aanmelden bij werk ruimte](./media/common/login-workspace.png)

Wanneer u uw werk ruimte hebt geopend, selecteert u de sectie **monitor** aan de linkerkant.

![Hub bewaken selecteren](./media/common/left-nav.png)

Selecteer **pijplijn uitvoeringen** om de lijst met pijplijn uitvoeringen weer te geven.

![Pijplijn uitvoeringen selecteren](./media/how-to-monitor-pipeline-runs/monitor-hub-nav-pipelineruns.png)

## <a name="filter-your-pipeline-runs"></a>De pijplijn uitvoeringen filteren

U kunt de lijst met pijplijn uitvoeringen filteren op degene waarin u bent geïnteresseerd. Met de filters boven aan het scherm kunt u een veld opgeven waarop u wilt filteren.

U kunt bijvoorbeeld de weer gave filteren om alleen de pijplijn uitvoeringen weer te geven voor de pijp lijn met de naam ' vakantie ':

![Knop filteren](./media/common/filter-button.png)

![Voorbeeld filter](./media/how-to-monitor-pipeline-runs/filter-example.png)

## <a name="view-details-about-a-specific-pipeline-run"></a>Details over een specifieke pijplijn uitvoering weer geven

Als u details over de pijplijn uitvoering wilt weer geven, selecteert u de pijplijn uitvoering. Bekijk vervolgens de uitvoeringen van de activiteit die zijn gekoppeld aan de pijplijn uitvoering. Als de pijp lijn nog steeds wordt uitgevoerd, kunt u de voortgang bewaken. 
  
## <a name="next-steps"></a>Volgende stappen

Zie het artikel [Apache Spark toepassingen bewaken](how-to-monitor-spark-applications.md) voor meer informatie over het bewaken van toepassingen. 
