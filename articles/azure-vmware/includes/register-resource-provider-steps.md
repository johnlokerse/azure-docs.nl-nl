---
title: De Azure VMware Solution-resourceprovider registreren
description: Stappen voor het registreren van de Azure VMware Solution-resourceprovider.
ms.topic: include
ms.date: 09/21/2020
ms.openlocfilehash: 96d15546c5102a69a0b19f92de33d35d2e9ab6c2
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/09/2020
ms.locfileid: "91575738"
---
<!-- Used in avs-deployment.md and tutorial-create-private-cloud.md -->

Als u Azure VMware Solution wilt gebruiken, moet u de resourceprovider eerst registreren bij uw abonnement.

```azurecli-interactive
az provider register -n Microsoft.AVS --subscription <your subscription ID>
```

>[!TIP]
>U kunt ook de GUI gebruiken om de **Micro soft.AVS**-resourceprovider te registreren.  Zie het artikel [Resourceprovider en typen registreren](../../azure-resource-manager/management/resource-providers-and-types.md#register-resource-provider) voor meer informatie.  
