---
title: Ondersteuning voor het verplaatsen van Azure SQL-resources tussen regio's met Azure resource-overschakeling.
description: Bekijk de ondersteuning voor het verplaatsen van Azure SQL-resources tussen regio's met Azure resource-overschakeling.
author: rayne-wiselman
manager: evansma
ms.service: resource-move
ms.topic: conceptual
ms.date: 09/07/2020
ms.author: raynew
ms.openlocfilehash: fda41a22c9bd9c66dd691b283ece10ac044db3ed
ms.sourcegitcommit: 96918333d87f4029d4d6af7ac44635c833abb3da
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/04/2020
ms.locfileid: "93324585"
---
# <a name="support-for-moving-azure-sql-resources-between-azure-regions"></a>Ondersteuning voor het verplaatsen van Azure SQL-resources tussen Azure-regio's

In dit artikel vindt u een overzicht van de ondersteuning en vereisten voor het verplaatsen van Azure SQL-resources tussen Azure-regio's met Azure resource-overschakeling.

## <a name="requirements"></a>Vereisten

In de volgende tabel vindt u een overzicht van de vereisten.

**Functie** | **Ondersteund/niet ondersteund** | **Details**
--- | --- | ---
**Azure SQL Database grootschalige** | Niet ondersteund | Kan geen data bases verplaatsen in de Azure SQL grootschalige-servicelaag met resource-overschakeling.
**Zoneredundantie** | Ondersteund |  Ondersteunde opties voor verplaatsen:<br/><br/> -Tussen regio's die ondersteuning bieden voor zone redundantie.<br/><br/> -Tussen regio's die geen zone redundantie ondersteunen.<br/><br/> -Tussen een regio die zone redundantie ondersteunt naar een regio die geen zone redundantie ondersteunt.<br/><br/> -Tussen een regio die geen ondersteuning biedt voor zone redundantie voor een regio die zone redundantie ondersteunt. 
**Gegevens synchronisatie** | Hub/synchronisatie database: niet ondersteund<br/><br/> Lid synchroniseren: ondersteund. | Als een Sync-lid wordt verplaatst, moet u de gegevens synchronisatie instellen voor de nieuwe doel database.
**Bestaande geo-replicatie** | Ondersteund | Bestaande geo-replica's worden opnieuw toegewezen aan de nieuwe primaire in de doel regio.<br/><br/> Seeding moet worden geïnitialiseerd na de verplaatsing. [Meer informatie](/azure/sql-database/sql-database-active-geo-replication-portal)
**Transparent Data Encryption (TDE) met Bring Your Own Key (BYOK)** | Ondersteund | Meer [informatie](../key-vault/general/move-region.md) over het verplaatsen van sleutel kluizen in verschillende regio's.
**TDE met door de service beheerde sleutel** | Ondersteund. |  Meer [informatie](../key-vault/general/move-region.md) over het verplaatsen van sleutel kluizen in verschillende regio's.
**Regels voor dynamische gegevens maskering** | Ondersteund. | Regels worden automatisch naar de doel regio gekopieerd als onderdeel van de verplaatsing. [Meer informatie](https://docs.microsoft.com/azure/sql-database/sql-database-dynamic-data-masking-get-started-portal).
**Advanced data security** | Niet ondersteund. | Tijdelijke oplossing: Stel in het doel gebied het SQL Server niveau in. [Meer informatie](https://docs.microsoft.com/azure/sql-database/sql-database-advanced-data-security).
**Firewall-regels** | Niet ondersteund. | Tijdelijke oplossing: Stel firewall regels in voor SQL Server in de doel regio. Firewall regels op database niveau worden van de bron server naar de doel server gekopieerd. [Meer informatie](https://docs.microsoft.com/azure/sql-database/sql-database-server-level-firewall-rule).
**Controle beleid** | Niet ondersteund. | Het beleid wordt na de verplaatsing opnieuw ingesteld op de standaard waarde. [Meer informatie](https://docs.microsoft.com/azure/sql-database/sql-database-auditing) over hoe u opnieuw kunt instellen.
**Back-upretentie** | Ondersteund. | Het bewaarbeleid voor back-ups van de brondatabase wordt meegenomen naar de doeldatabase. [Meer informatie](/azure/sql-database/sql-database-long-term-backup-retention-configure) over het wijzigen van instellingen na de verplaatsing.
**Automatisch afstemmen** | Niet ondersteund. | Tijdelijke oplossing: Stel de instellingen voor automatisch afstemmen in na de verplaatsing. [Meer informatie](https://docs.microsoft.com/azure/sql-database/sql-database-automatic-tuning-enable).
**Database waarschuwingen** | Niet ondersteund. | Tijdelijke oplossing: Stel waarschuwingen in na de verplaatsing. [Meer informatie](https://docs.microsoft.com/azure/sql-database/sql-database-insights-alerts-portal).
**Azure SQL Server stretch data base** | Niet ondersteund | Kan SQL Server stretch-data bases niet verplaatsen met resource-overdrijfing.
**Azure Synapse Analytics** | Niet ondersteund | Kan Synapse Analytics (voorheen SQL Data Warehouse) niet verplaatsen met resource-overboeking.
## <a name="next-steps"></a>Volgende stappen

Probeer [Azure SQL-resources](tutorial-move-region-sql.md) naar een andere regio met resource-overdrijfing.