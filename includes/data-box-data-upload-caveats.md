---
author: alkohli
ms.service: databox
ms.subservice: heavy
ms.topic: include
ms.date: 09/30/2020
ms.author: alkohli
ms.openlocfilehash: 80411ac191d0385ddafd4a3cc490d322ce039689
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/09/2020
ms.locfileid: "91639513"
---
- Kopieer bestanden niet rechtstreeks naar een van de voorgemaakte shares. U moet een map maken onder de share en vervolgens bestanden naar die map kopiëren.
- Een map onder de *StorageAccount_BlockBlob* en *StorageAccount_PageBlob* is een container. Zo worden bijvoorbeeld containers gemaakt als *StorageAccount_BlockBlob/container* en *StorageAccount_PageBlob/container*.
- Elke map die direct onder *StorageAccount_AzureFiles* wordt gemaakt, wordt vertaald naar een Azure-bestands share.
- Als een object dat wordt gekopieerd dezelfde naam heeft als een Azure-object, zoals een BLOB of een bestand, dat zich al in de Cloud bevindt, wordt het bestand in de Cloud overschreven door Data Box.
- Elk bestand dat in *StorageAccount_BlockBlob* is geschreven en *StorageAccount_PageBlob* shares wordt respectievelijk geüpload als een blok-Blob en een pagina-blob.
- Azure Blob-opslag biedt geen ondersteuning voor directory's. Als u een map in de map *StorageAccount_BlockBlob* maakt, worden virtuele mappen in de BLOB-naam gemaakt. Voor Azure Files wordt de daad werkelijke mapstructuur behouden.
- Een lege Directory-hiërarchie (zonder bestanden) die is gemaakt onder *StorageAccount_BlockBlob* en *StorageAccount_PageBlob* mappen worden niet geüpload.
- Als er fouten zijn bij het uploaden van gegevens naar Azure, wordt er een fouten logboek gemaakt in het doel-opslag account. Het pad naar dit fouten logboek is beschikbaar wanneer het uploaden is voltooid en u kunt het logboek controleren om de corrigerende actie te ondernemen. Verwijder geen gegevens uit de bron zonder de geüploade gegevens te verifiëren.
- Meta gegevens en NTFS-machtigingen voor bestanden kunnen worden bewaard wanneer de gegevens worden geüpload naar Azure Files met behulp van richt lijnen voor het behoud van de [acl's, kenmerken en tijds tempels van bestanden met Azure data Box](../articles/databox/data-box-file-acls-preservation.md).