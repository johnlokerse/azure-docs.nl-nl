---
title: 'PowerShell-voorbeeld: groep aan een toepassingsproxy-app toewijzen'
description: PowerShell-voorbeeld waarin een groep aan Azure Active Directory (Azure AD)-toepassingsproxytoepassing wordt toegewezen.
services: active-directory
author: kenwith
manager: CelesteDG
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.topic: sample
ms.date: 12/05/2019
ms.author: kenwith
ms.reviewer: japere
ms.openlocfilehash: 21dfb5794513ac3d811e34f64d00ecdba8db9de8
ms.sourcegitcommit: 8e7316bd4c4991de62ea485adca30065e5b86c67
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/17/2020
ms.locfileid: "94659179"
---
# <a name="assign-a-group-to-a-specific-azure-ad-application-proxy-application"></a>Een groep aan een bepaalde Azure AD-toepassingsproxytoepassing toewijzen

In dit PowerShell-voorbeeld kunt u een bepaalde groep aan een Azure Active Directory (Azure AD)-toepassingsproxytoepassing toewijzen.

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [updated-for-az](../../../../includes/updated-for-az.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Voor dit voorbeeld is de [AzureAD V2 PowerShell voor Graph-module](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0) (AzureAD) of de [AzureAD V2 PowerShell voor Graph-module (preview)](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0-preview) (AzureADPreview) vereist.

## <a name="sample-script"></a>Voorbeeldscript

[!code-azurepowershell[main](~/powershell_scripts/application-proxy/assign-group-to-app.ps1 "Assign a group to a specific Azure AD Application Proxy application")]

## <a name="script-explanation"></a>Uitleg van het script

| Opdracht | Opmerkingen |
|---|---|
| [New-AzureADGroupAppRoleAssignment](/powershell/module/AzureAD/New-azureadgroupapproleassignment?view=azureadps-2.0) | Hiermee wordt een groep aan een toepassingsrol toegewezen. |

## <a name="next-steps"></a>Volgende stappen

Zie het [overzicht van de Azure PowerShell-module](/powershell/azure/active-directory/overview?view=azureadps-2.0) voor meer informatie over de Azure AD PowerShell-module.

Zie [Azure AD PowerShell-voorbeelden voor de Azure AD-toepassingsproxy](../application-proxy-powershell-samples.md) voor andere PowerShell-voorbeelden voor de toepassingsproxy.