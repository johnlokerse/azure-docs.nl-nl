---
title: 'Zelfstudie: Azure Database for MySQL Flexible Server (preview-versie) en Azure App Service-web-app in hetzelfde virtuele netwerk maken'
description: Quickstart voor het maken van een Azure Database for MySQL Flexible Server (preview-versie) met web-app in een virtueel netwerk
author: mksuni
ms.author: sumuth
ms.service: mysql
ms.devlang: azurecli
ms.topic: tutorial
ms.date: 9/21/2020
ms.custom: mvc, devx-track-azurecli
ms.openlocfilehash: a7b673dc8dfeb2ebf86aec5b7449df91c2ffd635
ms.sourcegitcommit: d767156543e16e816fc8a0c3777f033d649ffd3c
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/26/2020
ms.locfileid: "92534053"
---
# <a name="tutorial-create-an-azure-database-for-mysql---flexible-server-preview-with-app-services-web-app-in-virtual-network"></a>Zelfstudie: Azure Database for MySQL - Flexible Server (preview-versie) met App Services-web-app in een virtueel netwerk maken

> [!IMPORTANT]
> Azure Database for MySQL - Flexible Server is momenteel beschikbaar als openbare preview.

In deze zelfstudie leert u hoe u een Azure App Service-web-app met MySQL Flexible Server (preview-versie) in een [virtueel netwerk](../../virtual-network/virtual-networks-overview.md) maakt.

## <a name="prerequisites"></a>Vereisten

Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.

In dit artikel moet u Azure CLI-versie 2.0 of later lokaal uitvoeren. Voer de opdracht `az --version` uit om de geïnstalleerde versie te zien. Zie [Azure CLI installeren](/cli/azure/install-azure-cli) als u de CLI wilt installeren of een upgrade wilt uitvoeren.

U moet zich aanmelden bij uw account met behulp van de opdracht [az login](/cli/azure/reference-index#az-login). Let op de **id** -eigenschap van de opdrachtuitvoer voor de naam van het desbetreffende abonnement.

```azurecli
az login
```

Als u meerdere abonnementen hebt, kiest u het juiste abonnement waarin de resource moet worden gefactureerd. Selecteer de specifieke abonnements-id in uw account met de opdracht [az account set](/cli/azure/account). Gebruik de eigenschap **abonnement-id** uit de **az login** -uitvoer voor uw abonnement in de tijdelijke aanduiding voor de abonnement-id.

```azurecli
az account set --subscription <subscription id>
```

## <a name="create-an-azure-database-for-mysql-flexible-server"></a>Een Azure Database for MySQL Flexible Server maken

Maak een flexibele privéserver in een virtueel netwerk (VNET) met behulp van de volgende opdracht:
```azurecli
az mysql flexible-server create --resource-group myresourcegroup --location westus2
```
Deze opdracht voert de volgende acties uit, dit kan enkele minuten duren:

- Maak de resourcegroep als deze nog niet bestaat.
- Hiermee wordt een servernaam gegenereerd als deze niet wordt opgegeven.
- Maak een nieuw virtueel netwerk voor de nieuwe MySQL-server. Noteer de naam van het virtuele netwerk en het subnet dat voor uw server is gemaakt. U moet de web-app namelijk aan hetzelfde virtuele netwerk toevoegen.
- Hiermee maakt u de gebruikersnaam van de beheerder en het wachtwoord voor uw server indien niet opgegeven.
- Hiermee maakt u een lege database met de naam **flexibleserverdb**

> [!NOTE]
> Noteer het wachtwoord dat voor u wordt gegenereerd als het niet is opgegeven. Als u het wachtwoord vergeet, kunt u het wachtwoord opnieuw instellen met behulp van de opdracht ``` az mysql flexible-server update```

## <a name="create-a-web-app"></a>Een webtoepassing maken

In dit gedeelte maakt u een app-host in een App Service-app en verbindt u deze app met de MySQL-database. Controleer of u zich in de hoofdmap bevindt van de opslagplaats die de code van de app bevat.

Een App Service-app maken (het hostproces) met de opdracht az webapp up

```azurecli
az webapp up --resource-group myresourcegroup --location westus2 --plan testappserviceplan --sku B1 --name mywebapp
```

> [!NOTE]
> - Gebruik voor het locatieargument -- dezelfde locatie als voor de database in het vorige gedeelte.
> - Vervang _&lt;app-name>_ door een unieke naam in heel Azure (het servereindpunt is https://\<app-name>.azurewebsites.net). Geldige tekens voor <app-name> zijn: a-z, 0-9, en -. Het is handig om een een combinatie van uw bedrijfsnaam en een app-id te gebruiken.

Deze opdracht voert de volgende acties uit, dit kan enkele minuten duren:

- Maak de resourcegroep als deze nog niet bestaat. (In deze opdracht gebruikt u dezelfde resourcegroep waarin u de database eerder hebt gemaakt.)
- Maak het App Service-plan ```testappserviceplan``` in de prijscategorie Basic (B1), als het nog niet bestaat. --plan en --sku zijn optioneel.
- Maak de App Service-app als deze nog niet bestaat.
- Schakel standaardlogboeken voor de app in, als die nog niet zijn ingeschakeld.
- Upload de opslagplaats met behulp van ZIP-implementatie, met ingeschakelde bouwautomatisering.

## <a name="add-the-web-app-to-the-virtual-network"></a>De web-app toevoegen aan het virtuele netwerk

Gebruik de opdracht **az webapp vnet-integration** om een regionale virtuele netwerkintegratie toe te voegen aan een webapp. Vervang _&lt;vnet-name>_ en _&lt;subnet-name_ door het virtuele netwerk en de naam van het subnet die de flexibele server gebruikt.

```azurecli
az webapp vnet-integration add -g myresourcegroup -n  mywebapp --vnet <vnet-name> --subnet <subnet-name>
```

## <a name="configure-environment-variables-to-connect-the-database"></a>De omgevingsvariabelen configureren om de database te verbinden

Nu de code is geïmplementeerd naar App Service, is de volgende stap het verbinden van de app met de flexibele server in Azure. De code van de app verwacht om database-informatie te vinden in een aantal omgevingsvariabelen. Om omgevingsvariabelen in te stellen in App Service, maakt u 'app-instellingen' met de SET-opdracht ```az webapp config appsettings```.

```azurecli
az webapp config appsettings set --settings DBHOST="<mysql-server-name>.mysql.database.azure.com" DBNAME="flexibleserverdb" DBUSER="<username>" DBPASS="<password>"
```

- Vervang _&lt;mysql-server-name>_ , _&lt;username>_ en _&lt;password>_ voor de zojuist gemaakte opdracht voor de flexibele server.
- Vervang _&lt;username>_ en _&lt;password>_ door de referenties die ook door de opdracht voor u zijn gegenereerd.
- De resourcegroep en de naam van de app worden opgehaald uit de cachewaarden in het bestand . azure/config.
- Met de opdracht worden instellingen gemaakt met de naam DBHOST, DBNAME, DBUSER en DBPASS. Als uw toepassingscode een andere naam gebruikt voor de databasegegevens, gebruikt u deze namen voor de app-instellingen zoals vermeld in de code.

## <a name="clean-up-resources"></a>Resources opschonen

Verwijder alle resources die u hebt gemaakt in de zelfstudie met behulp van de volgende opdracht. Met deze opdracht verwijdert u alle resources in deze resourcegroep.

```azurecli
az group delete -n myresourcegroup
```

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Een bestaande aangepaste DNS-naam toewijzen aan Azure App Service](../../app-service/app-service-web-tutorial-custom-domain.md)