---
title: Inzicht in korting voor gereserveerde Dedicated Host-instanties voor in Azure
description: Meer informatie over hoe korting voor gereserveerde VM-instanties in Azure wordt toegepast op Azure Dedicated Hosts.
author: yashesvi
ms.service: cost-management-billing
ms.subservice: reservations
ms.topic: conceptual
ms.date: 02/28/2020
ms.author: banders
ms.openlocfilehash: 8d273aae3588a006f7b0a55d2798b7a43c040c9b
ms.sourcegitcommit: dbe434f45f9d0f9d298076bf8c08672ceca416c6
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/17/2020
ms.locfileid: "92148371"
---
# <a name="how-the-azure-reservation-discount-is-applied-to-azure-dedicated-hosts"></a>Hoe korting voor Azure-reserveringen wordt toegepast op Azure Dedicated Hosts

Wanneer u een gereserveerde Dedicated Host-instantie in Azure aanschaft, wordt de reserveringskorting automatisch toegepast op toegewezen hosts die overeenkomen met de kenmerken en hoeveelheid van de reservering. Een reservering dekt de rekenkosten van uw toegewezen hosts.

## <a name="how-reservation-discount-is-applied"></a>De manier waarop reserveringskorting wordt toegepast

Voor een reserveringskorting geldt: '*gebruiken of verliezen*'. Als u voor een bepaald uur geen passende resources hebt, verliest u de reserveringshoeveelheid voor dat uur. U kunt ongebruikte gereserveerde uren niet meenemen.

Wanneer u een toegewezen host verwijdert, wordt de reserveringskorting automatisch toegepast op een andere overeenkomstige resource in het opgegeven bereik. Als er geen overeenkomstige resources in het opgegeven bereik worden gevonden, *verliest* u de gereserveerde uren.

## <a name="reservation-discount-for-dedicated-hosts"></a>Reserveringskorting voor toegewezen hosts

Met gereserveerde Azure-instanties voor toegewezen hosts krijgt u korting op de kosten van de compute-infrastructuur die wordt gebruikt voor uw toegewezen hosts. De korting geldt voor uw toegewezen hosts, ongeacht of deze worden gebruikt door virtuele machines of niet. De reservering geldt niet voor extra kosten zoals licenties, netwerkgebruik of opslaggebruik door virtuele machines die op de toegewezen host zijn geïmplementeerd.

## <a name="need-help-contact-us"></a>Hebt u hulp nodig? Contact opnemen

Als u vragen hebt of hulp nodig hebt,  [kunt u een ondersteuningsaanvraag maken](https://go.microsoft.com/fwlink/?linkid=2083458).

## <a name="next-steps"></a>Volgende stappen

Raadpleeg de volgende artikelen voor meer informatie over Azure-reserveringen:

- [Wat zijn reserveringen voor Azure?](./save-compute-costs-reservations.md)

- [Azure Dedicated Host gebruiken](../../virtual-machines/dedicated-hosts.md)

- [Prijzen van Dedicated Host](https://azure.microsoft.com/pricing/details/virtual-machines/dedicated-host/)

- [Reserveringen voor Azure beheren](./manage-reserved-vm-instance.md)

- [Inzicht in het gebruik van reserveringen voor uw abonnement met betalen per gebruik](./understand-reserved-instance-usage.md)

- [Inzicht in het gebruik van reserveringen voor Enterprise-inschrijvingen](./understand-reserved-instance-usage-ea.md)

- [Inzicht in het gebruik van reserveringen voor CSP-abonnementen](/partner-center/azure-reservations)