---
title: Strategieën voor gegevenstoegang
description: Azure Data Factory ondersteunt nu vaste IP-adresbereiken.
services: data-factory
ms.author: abnarain
author: nabhishek
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.date: 05/28/2020
ms.openlocfilehash: 785381e0a42f2b502e4ea7054753d5f3fb67f385
ms.sourcegitcommit: fb3c846de147cc2e3515cd8219d8c84790e3a442
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/27/2020
ms.locfileid: "92632767"
---
# <a name="data-access-strategies"></a>Strategieën voor gegevenstoegang

[!INCLUDE[appliesto-adf-asa-md](includes/appliesto-adf-asa-md.md)]

Een cruciaal beveiligings doel van een organisatie is het beveiligen van hun gegevens archieven via internet, maar dit is mogelijk een on-premises of een Cloud/SaaS-gegevens archief. 

Normaal gesp roken beheert een gegevens archief in de Cloud de toegang met behulp van de onderstaande mechanismen:
* Persoonlijke koppeling van een Virtual Network naar gegevens bronnen met persoonlijke eind punten ingeschakeld
* Firewall regels die de connectiviteit beperken op basis van het IP-adres
* Verificatie mechanismen waarvoor gebruikers hun identiteit moeten bewijzen
* Autorisatie mechanismen waarmee gebruikers worden beperkt tot specifieke acties en gegevens

> [!TIP]
> Met de [introductie van een statisch IP-adres bereik](./azure-integration-runtime-ip-addresses.md)kunt u nu IP-adresbereiken voor de specifieke Azure Integration runtime-regio toestaan om ervoor te zorgen dat u niet alle Azure IP-adressen in uw gegevens archieven in de cloud kunt toestaan. Op deze manier kunt u de IP-adressen beperken die zijn toegestaan voor toegang tot de gegevens archieven.

> [!NOTE] 
> De IP-adresbereiken worden geblokkeerd voor Azure Integration Runtime en worden momenteel alleen gebruikt voor gegevens verplaatsing, pijp lijn en externe activiteiten. Gegevens stromen en Azure Integration Runtime waarmee beheerde Virtual Network nu geen gebruik maken van deze IP-bereiken. 

Dit kan in veel scenario's werken en we begrijpen dat een uniek, statisch IP-adres per Integration runtime gewenst zou zijn, maar dit zou niet mogelijk kunnen zijn met behulp van Azure Integration Runtime op dit moment zonder server. Indien nodig kunt u altijd een zelf-hostende Integration Runtime instellen en uw statische IP-adres gebruiken. 

## <a name="data-access-strategies-through-azure-data-factory"></a>Strategieën voor gegevens toegang via Azure Data Factory

* **[Privé-koppeling](../private-link/private-link-overview.md)** : u kunt een Azure Integration runtime maken binnen Azure Data Factory beheerde Virtual Network en maakt gebruik van privé-eind punten om een beveiligde verbinding te maken met ondersteunde gegevens archieven. Verkeer tussen beheerde Virtual Network en gegevens bronnen wordt het micro soft-backbone-netwerk verplaatst en worden niet blootgesteld aan een openbaar netwerk.
* **[Trusted service](../storage/common/storage-network-security.md#exceptions)** -Azure Storage (Blob, ADLS Gen2) ondersteunt firewall configuratie waarmee betrouw bare Azure-platform Services kunnen worden geselecteerd om veilig toegang te krijgen tot het opslag account. Vertrouwde services afdwingt beheerde identiteits verificatie, zodat er geen andere data factory verbinding kan maken met deze opslag, tenzij dit wordt goedgekeurd met behulp van de beheerde identiteit. U vindt meer informatie in **[deze blog](https://techcommunity.microsoft.com/t5/azure-data-factory/data-factory-is-now-a-trusted-service-in-azure-storage-and-azure/ba-p/964993)** . Dit is daarom zeer veilig en wordt aanbevolen. 
* **Uniek statisch IP** -u moet een zelf-hostende Integration runtime instellen om een statisch IP-adres voor Data Factory-connectors te krijgen. Dit mechanisme zorgt ervoor dat u de toegang tot alle andere IP-adressen kunt blok keren. 
* **[Statisch IP-bereik](./azure-integration-runtime-ip-addresses.md)** : u kunt IP-adressen van Azure Integration runtime gebruiken om deze in uw opslag ruimte weer te geven (bijvoorbeeld S3, Sales Force, enz.). Het is zeker dat IP-adressen die verbinding kunnen maken met de gegevens archieven worden beperkt, maar ook afhankelijk zijn van verificatie-en autorisatie regels.
* **[Servicetag: een](../virtual-network/service-tags-overview.md)** service label vertegenwoordigt een groep IP-adres voorvoegsels van een bepaalde Azure-service (zoals Azure Data Factory). Micro soft beheert de adres voorvoegsels die zijn opgenomen in het servicetag en werkt de servicetag automatisch bij met gewijzigde adressen, zodat de complexiteit van regel matige updates voor netwerk beveiligings regels wordt geminimaliseerd. Het is handig bij het filteren van gegevens toegang op IaaS-gehoste gegevens archieven in Virtual Network.
* **Azure-Services toestaan** : met sommige services kunt u alle Azure-Services verbinding laten maken voor het geval u deze optie kiest. 

Zie onder twee tabellen voor meer informatie over ondersteunde netwerk beveiligings mechanismen voor gegevens archieven in Azure Integration Runtime en zelf-hostende Integration Runtime.  
* **Azure Integration Runtime**

    | Gegevensarchieven                  | Ondersteund netwerk beveiligings mechanisme in gegevens archieven | Private Link     | Vertrouwde service     | Statisch IP-bereik | Servicetags | Azure-Services toestaan |
    |------------------------------|-------------------------------------------------------------|---------------------|-----------------|--------------|----------------------|-----------------|
    | Azure PaaS-gegevens opslag       | Azure Cosmos DB                                     | Ja              | -                   | Ja             | -            | Ja                  |
    |                              | Azure Data Explorer                                 | -                | -                   | Ja*            | Ja*         | -                    |
    |                              | Azure Data Lake gen1                                | -                | -                   | Ja             | -            | Ja                  |
    |                              | Azure Database for MariaDB, MySQL, PostgreSQL       | -                | -                   | Ja             | -            | Ja                  |
    |                              | Azure File Storage                                  | Ja              | -                   | Ja             | -            | .                    |
    |                              | Azure Storage (BLOB, ADLS Gen2)                     | Ja              | Ja (alleen MSI-verificatie) | Ja             | -            | .                    |
    |                              | Azure SQL DB, Azure Synapse Analytics), SQL ml  | Ja (alleen Azure SQL DB/DW)        | -                   | Ja             | -            | Ja                  |
    |                              | Azure Key Vault (voor het ophalen van geheimen/connection string) | ja      | Ja                 | Ja             | -            | -                    |
    | Andere PaaS/SaaS-gegevens archieven | AWS S3, Sales Force, Google Cloud Storage, enzovoort.    | -                | -                   | Ja             | -            | -                    |
    | Azure-laaS                   | SQL Server, Oracle, etc.                          | -                | -                   | Ja             | Ja          | -                    |
    | On-premises laaS              | SQL Server, Oracle, etc.                          | -                | -                   | Ja             | -            | -                    |
    
    **Alleen van toepassing als Azure Data Explorer virtueel netwerk is geïnjecteerd en IP-bereik kan worden toegepast op NSG/firewall.* 

* **Zelf-hostende Integration Runtime (in Vnet/on-premises)**
    
    | Gegevens archieven                  | Ondersteund netwerk beveiligings mechanisme in gegevens archieven         | Statisch IP-adres | Vertrouwde services  |
    |--------------------------------|---------------------------------------------------------------|-----------|---------------------|
    | Azure PaaS-gegevens opslag       | Azure Cosmos DB                                               | Ja       | -                   |
    |                                | Azure Data Explorer                                           | -         | -                   |
    |                                | Azure Data Lake gen1                                          | Ja       | -                   |
    |                                | Azure Database for MariaDB, MySQL, PostgreSQL               | Ja       | -                   |
    |                                | Azure File Storage                                            | Ja       | -                   |
    |                                | Azure Storage (blog, ADLS Gen2)                             | Ja       | Ja (alleen MSI-verificatie) |
    |                                | Azure SQL DB, Azure Synapse Analytics), SQL ml          | Ja       | -                   |
    |                                | Azure Key Vault (voor het ophalen van geheimen/connection string) | Ja       | Ja                 |
    | Andere PaaS/SaaS-gegevens archieven | AWS S3, Sales Force, Google Cloud Storage, enzovoort.              | Ja       | -                   |
    | Azure-laaS                     | SQL Server, Oracle, etc.                                  | Ja       | -                   |
    | On-premises laaS              | SQL Server, Oracle, etc.                                  | Ja       | -                   |    

## <a name="next-steps"></a>Volgende stappen

Zie de volgende verwante artikelen voor meer informatie:
* [Ondersteunde gegevensarchieven](./copy-activity-overview.md#supported-data-stores-and-formats)
* [Vertrouwde services Azure Key Vault](../key-vault/general/overview-vnet-service-endpoints.md#trusted-services)
* [Vertrouwde micro soft-Services Azure Storage](../storage/common/storage-network-security.md#trusted-microsoft-services)
* [Beheerde identiteit voor Data Factory](./data-factory-service-identity.md)