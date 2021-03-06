---
title: Infra structuur dubbele versleuteling-Azure Database for MySQL
description: Meer informatie over het gebruik van een infra structuur met dubbele versleuteling om een tweede laag versleuteling toe te voegen met een door de service beheerde sleutels.
author: mksuni
ms.author: sumuth
ms.service: mysql
ms.topic: conceptual
ms.date: 6/30/2020
ms.openlocfilehash: 233dcbeee0bccc714e3b4fe93e7c8b19aa9f2df0
ms.sourcegitcommit: 80034a1819072f45c1772940953fef06d92fefc8
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93242446"
---
# <a name="azure-database-for-mysql-infrastructure-double-encryption"></a>Dubbele versleuteling van Azure Database for MySQL-infra structuur

Azure Database for MySQL maakt gebruik van opslag [versleuteling van gegevens op rest](concepts-security.md#at-rest) voor gegevens met behulp van de door micro soft beheerde sleutels. Gegevens, met inbegrip van back-ups, worden versleuteld op schijf en deze versleuteling is altijd ingeschakeld en kan niet worden uitgeschakeld. De versleuteling maakt gebruik van FIPS 140-2-gevalideerde cryptografische modules en een AES 256-bits code ring voor de versleuteling van Azure Storage.

Infrastructuur dubbele versleuteling voegt een tweede laag versleuteling toe met door service beheerde sleutels. Er wordt gebruikgemaakt van de FIPS 140-2-gevalideerde cryptografische module, maar met een ander versleutelings algoritme. Dit biedt een extra beveiligingslaag voor uw gegevens in rust. De sleutel die in de infra structuur met dubbele versleuteling wordt gebruikt, wordt ook beheerd door de Azure Database for MySQL-service. De infra structuur met dubbele versleuteling is niet standaard ingeschakeld, omdat de extra versleutelings versleuteling de prestaties kan beïnvloeden.

> [!NOTE]
> Deze functie wordt alleen ondersteund voor de prijs Categorieën Algemeen en geoptimaliseerd voor geheugen in Azure Database for PostgreSQL.

Infrastructuur laag versleuteling biedt het voor deel dat wordt geïmplementeerd op de laag die het dichtst bij het opslag apparaat of netwerk draden ligt. Azure Database for MySQL implementeert de twee coderings lagen met door service beheerde sleutels. Hoewel u nog steeds technisch in de service slaag bent, wordt het zeer dicht bij de hardware die de gegevens in rust opslaat. U kunt nog steeds gegevens versleuteling op rest inschakelen met behulp van de door de [klant beheerde sleutel](concepts-data-encryption-mysql.md) voor de ingerichte mysql-server. 

Implementatie op de infrastructuur lagen ondersteunt ook een verscheidenheid aan sleutels. Infra structuur moet rekening houden met verschillende clusters van computers en netwerken. Als zodanig worden verschillende sleutels gebruikt om de versterking van de infra structuur van infrastructuur aanvallen en een groot aantal hardware en netwerk fouten te minimaliseren. 

> [!NOTE]
> Het gebruik van een infra structuur met dubbele versleuteling heeft invloed op de prestaties van de Azure Database for MySQL-server vanwege het aanvullende versleutelings proces.

## <a name="benefits"></a>Voordelen

Infra structuur dubbele versleuteling voor Azure Database for MySQL biedt de volgende voor delen:

1. **Extra diversiteit van crypto grafie** -de geplande overgang naar op hardware gebaseerde versleuteling zal de implementaties verder spreiden door een implementatie op basis van de software te bieden, naast de implementatie op basis van toepassingen.
2. **Implementatie fouten** -twee versleutelings lagen op infrastructuur laag worden beschermd tegen fouten in de cache of het geheugen beheer in hogere lagen die gegevens over de Lees bare tekst weer gegeven. Daarnaast zorgt de twee lagen er ook voor dat er fouten optreden in de implementatie van de versleuteling in het algemeen.

De combi natie van deze biedt een zware beveiliging tegen veelvoorkomende bedreigingen en zwakke plekken die worden gebruikt voor de aanval van crypto grafie.

## <a name="supported-scenarios-with-infrastructure-double-encryption"></a>Ondersteunde scenario's met dubbele infra structuur versleuteling

De versleutelings mogelijkheden die door Azure Database for MySQL worden geboden, kunnen samen worden gebruikt. Hieronder vindt u een overzicht van de verschillende scenario's die u kunt gebruiken:

|  ##   | Standaard versleuteling | Dubbele infrastructuurversleuteling | Gegevens versleuteling met door de klant beheerde sleutels  |
|:------|:------------------:|:--------------------------------:|:--------------------------------------------:|
| 1     | *Ja*              | *Nee*                             | *Nee*                                         |
| 2     | *Ja*              | *Ja*                            | *Nee*                                         |
| 3     | *Ja*              | *Nee*                             | *Ja*                                        |
| 4     | *Ja*              | *Ja*                            | *Ja*                                        |
|       |                    |                                  |                                              |

> [!Important]
> - Scenario 2 en 4 kunnen een door Voer van 5-10 procent veroorzaken op basis van het type werk belasting voor Azure Database for MySQL server vanwege de extra laag van infrastructuur versleuteling.
> - Het configureren van een infra structuur met dubbele versleuteling voor Azure Database for MySQL is alleen toegestaan tijdens het maken van de server. Zodra de server is ingericht, kunt u de opslag versleuteling niet meer wijzigen. U kunt echter nog steeds gegevens versleuteling inschakelen met behulp van door de klant beheerde sleutels voor de server die is gemaakt met/zonder een infra structuur met dubbele code ring.

## <a name="limitations"></a>Beperkingen

Voor Azure Database for MySQL heeft de ondersteuning voor infra structuur met dubbele versleuteling met door de service beheerde sleutel de volgende beperkingen:

* Ondersteuning voor deze functionaliteit is beperkt tot de prijs categorie **Algemeen** en **geoptimaliseerd voor geheugen** .
* U kunt een Azure Database for MySQL maken waarop infrastructuur versleuteling is ingeschakeld in de volgende regio's:

   * VS - oost
   * VS - zuid-centraal
   * US - west 2
   
* * Deze functie wordt alleen ondersteund in regio's en servers, die ondersteuning bieden voor opslag tot Maxi maal 16 TB. Raadpleeg de [opslag documentatie](concepts-pricing-tiers.md#storage)voor de lijst met Azure-regio's die ondersteuning bieden voor opslag tot 16 TB.

    > [!NOTE]
    > - Alle **nieuwe** mysql-servers die zijn gemaakt in de hierboven vermelde regio's, ondersteunen ook de versleuteling van gegevens met klant Manager-sleutels. In dit geval komen servers die zijn gemaakt via PITR (Point-in-time Restore) of lees replica's niet in aanmerking als ' nieuw '.
    > - Als u wilt valideren of uw ingerichte server tot 16 TB ondersteunt, gaat u naar de Blade prijs categorie in de portal en controleert u of de schuif regelaar voor opslag kan worden verplaatst naar 16 TB. Als u de schuif regelaar alleen kunt verplaatsen naar 4 TB, ondersteunt uw server mogelijk geen versleuteling met door de klant beheerde sleutels. de gegevens worden echter te allen tijde versleuteld met behulp van door de service beheerde sleutels. Neem contact op met AskAzureDBforMySQL@service.microsoft.com Als u vragen hebt.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over het [instellen van een infra structuur met dubbele versleuteling voor Azure data base for MySQL](howto-double-encryption.md).
