---
title: NCas T4 v3-serie
description: Specificaties voor de virtuele machines uit de NCas T4 v3-serie.
services: virtual-machines
ms.subservice: sizes
author: vikancha-MSFT
ms.service: virtual-machines
ms.topic: conceptual
ms.date: 08/10/2020
ms.author: vikancha
ms.openlocfilehash: 7c3423e8bd5cd3e38c05205842845bec2243ed83
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/09/2020
ms.locfileid: "91653499"
---
# <a name="ncast4_v3-series-in-preview"></a>NCasT4_v3-serie (in preview-versie) 

De virtuele machines uit de NCasT4_v3-serie worden aangedreven door [Nvidia Tesla T4](https://www.nvidia.com/en-us/data-center/tesla-t4/) GPU'S en AMD EPYC 7V12 (Rome) cpu's. De virtuele machines beschikken over Maxi maal 4 NVIDIA T4-Gpu's met 16 GB geheugen per, Maxi maal 64 niet-multi threaded AMD EPYC 7V12 (Rome)-processor kernen en 440 GiB van het systeem geheugen. Deze virtuele machines zijn ideaal voor het implementeren van AI-Services, zoals realtime deprocessoren van door de gebruiker gegenereerde aanvragen of voor interactieve grafische en visualisatie werk belastingen met behulp van het GRID-stuur programma en virtuele GPU-technologie van NVIDIA. Standaard GPU Compute-workloads op basis van CUDA, TensorRT, Caffe, ONNX en andere frameworks of GPU-versnelde grafische toepassingen op basis van OpenGL en DirectX kunnen economisch worden geïmplementeerd, met dichtbij de buurt van gebruikers op de NCasT4_v3 serie.

> [!NOTe]
> [Dien een aanvraag](https://aka.ms/NCT4v3Preview) in als onderdeel van het preview-programma.

<br>

[ACU](acu.md): 230-260<br>
[Premium Storage](premium-storage-performance.md): ondersteund<br>
[Premium Storage caching](premium-storage-performance.md): ondersteund<br>
[Livemigratie](maintenance-and-updates.md): niet ondersteund<br>
[Updates](maintenance-and-updates.md)voor het behouden van geheugen: niet ondersteund<br>
[Ondersteuning](generation-2.md)voor het genereren van vm's: generatie 1<br>
<br>

| Grootte | vCPU | Geheugen: GiB | Tijdelijke opslag (SSD) GiB | GPU | GPU-geheugen: GiB | Max. aantal gegevensschijven | Max. aantal NIC's |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_NC4as_T4_v3 |4 |28 |180 | 1 | 16 | 8 | 2 |
| Standard_NC8as_T4_v3 |8 |56 |360 | 1 | 16 | 16 | 4  |
| Standard_NC16as_T4_v3 |16 |110 |360 | 1 | 16 | 32 | 8  |
| Standard_NC64as_T4_v3 |64 |440 |2880 | 4 | 64 | 32 | 8  |


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../includes/virtual-machines-common-sizes-table-defs.md)]

## <a name="supported-operating-systems-and-drivers"></a>Ondersteunde besturingssystemen en stuurprogramma’s

Als u gebruik wilt maken van de GPU-mogelijkheden van Azure NCasT4_v3-serie Vm's waarop Windows of Linux wordt uitgevoerd, moeten de NVIDIA GPU-Stuur Programma's zijn geïnstalleerd.

Als u de NVIDIA GPU-Stuur Programma's hand matig wilt installeren, raadpleegt u [N-Series GPU-stuur programma-installatie voor Windows](./windows/n-series-driver-setup.md) voor ondersteunde besturings systemen, stuur Programma's, installatie en verificaties tappen.

## <a name="other-sizes"></a>Andere grootten

- [Algemeen doel](sizes-general.md)
- [Geoptimaliseerd geheugen](sizes-memory.md)
- [Geoptimaliseerde opslag](sizes-storage.md)
- [Geoptimaliseerde GPU](sizes-gpu.md)
- [Krachtig rekenvermogen](sizes-hpc.md)
- [Vorige generaties](sizes-previous-gen.md)

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe [Azure Compute units (ACU)](acu.md) u kan helpen bij het vergelijken van de reken prestaties in azure-sku's.
