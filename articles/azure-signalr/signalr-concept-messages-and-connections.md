---
title: Berichten en verbindingen in Azure SignalR Service
description: Een overzicht van de belangrijkste concepten over berichten en verbindingen in Azure SignalR Service.
author: sffamily
ms.service: signalr
ms.topic: conceptual
ms.date: 08/05/2020
ms.author: zhshang
ms.openlocfilehash: d71462bd30dbd4b377353c792a3c579e02949680
ms.sourcegitcommit: dbe434f45f9d0f9d298076bf8c08672ceca416c6
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/17/2020
ms.locfileid: "92151091"
---
# <a name="messages-and-connections-in-azure-signalr-service"></a>Berichten en verbindingen in Azure SignalR Service

Het factureringsmodel voor Azure SignalR Service is gebaseerd op het aantal verbindingen en het aantal berichten. In dit artikel wordt uitgelegd hoe berichten en verbindingen worden gedefinieerd en geteld voor factureringsdoeleinden.


## <a name="message-formats"></a>Berichtindelingen 

De Azure signalerings service ondersteunt dezelfde indelingen als ASP.NET Core-Signa lering: [JSON](https://www.json.org/) en [Message Pack](/aspnet/core/signalr/messagepackhubprotocol).

## <a name="message-size"></a>Berichtgrootte

Azure SignalR Service heeft geen groottelimiet voor berichten.

Grote berichten worden opgesplitst in kleinere berichten van elke maximaal 2 kB, die als afzonderlijke berichten worden verzonden. Het splitsen en samenvoegen van berichten wordt afgehandeld via SDK's. Ontwikkelaars hoeven er niets voor te doen.

Grote berichten hebben een negatieve invloed op de prestaties van de berichtenafhandeling. Gebruik, indien mogelijk, kleinere berichten en voer tests uit om de optimale berichtgrootte voor elk gebruiksscenario te bepalen.

## <a name="how-messages-are-counted-for-billing"></a>Hoe berichten worden meegeteld voor de facturering

Voor de facturering worden alleen uitgaande berichten van Azure SignalR Service meegeteld. Ping-berichten tussen clients en servers worden genegeerd.

Een bericht dat groter is dan 2 kB, wordt beschouwd als meerdere berichten van elk 2 kB. De grafiek met het aantal berichten in de Azure-portal wordt elke 100 berichten per hub bijgewerkt.

Stel bijvoorbeeld dat u één toepassings server hebt en drie clients:

App server verzendt een bericht van 1 KB naar alle verbonden clients, het bericht van de app-server naar de service wordt beschouwd als een beschikbaar binnenkomend bericht. Alleen de drie berichten die vanuit de service naar elk van de client worden verzonden, worden als uitgaande berichten gefactureerd.

Client A stuurt een bericht van 1 KB naar een andere client B, zonder de app server te passeren. Het bericht van client A naar-service is gratis binnenkomend bericht. Het bericht van de service naar client B wordt gefactureerd als uitgaand bericht.

Als u drie clients en één toepassings server hebt. Vanaf één client wordt een bericht van 4 kB verzonden dat via de server moet worden uitgezonden naar alle clients. Het aantal gefactureerde berichten is acht: één bericht van de service naar de toepassings server en drie berichten van de service naar de clients. Elk bericht wordt geteld als twee berichten van 2 kB.

## <a name="how-connections-are-counted"></a>Hoe verbindingen worden geteld

Er zijn server verbindingen en client verbindingen met de Azure signalerings service. Standaard begint elke toepassings server met vijf initiële verbindingen per hub, en elke client heeft één client verbinding.

Het aantal verbindingen dat in de Azure-portal wordt weergegeven, betreft zowel server- als clientverbindingen.

Stel dat u twee toepassings servers hebt en u vijf hubs in code definieert. Het aantal server verbindingen is 50:2 app-servers * 5 hubs * 5 verbindingen per hub.

ASP.NET SignalR berekent serververbindingen op een andere manier. Het bevat één standaardhub, naast de hubs die u definieert. Standaard moet elke toepassings server vijf extra initiële server verbindingen hebben. Het oorspronkelijke aantal verbindingen voor de standaard-hub blijft consistent met andere hubs.

De service en de toepassings server blijven synchroniseren van de verbindings status en maken aanpassing van server verbindingen om betere prestaties en stabiliteit van de service te verkrijgen.  Het is dus mogelijk dat de server verbindings nummers van tijd tot tijd veranderen.

## <a name="how-inboundoutbound-traffic-is-counted"></a>Hoe binnenkomend/uitgaand verkeer wordt geteld

Het bericht dat naar de service wordt verzonden, is een inkomend bericht. Het bericht dat vanuit de service wordt verzonden, is een uitgaand bericht. Verkeer wordt geteld in bytes.

## <a name="related-resources"></a>Gerelateerde resources

- [Aggregatietypen in Azure Monitor](../azure-monitor/platform/metrics-supported.md#microsoftsignalrservicesignalr )
- [ASP.NET Core SignalR-configuratie](/aspnet/core/signalr/configuration)
- [JSON](https://www.json.org/)
- [MessagePack](/aspnet/core/signalr/messagepackhubprotocol)