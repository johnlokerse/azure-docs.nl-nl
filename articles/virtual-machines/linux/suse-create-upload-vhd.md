---
title: Een SUSE Linux-VHD maken en uploaden in azure
description: Meer informatie over het maken en uploaden van een virtuele harde schijf (VHD) van Azure die een SUSE Linux-besturings systeem bevat.
author: gbowerman
ms.service: virtual-machines-linux
ms.subservice: imaging
ms.workload: infrastructure-services
ms.topic: how-to
ms.date: 03/12/2018
ms.author: guybo
ms.openlocfilehash: 1f35adcc797e903bb44852e9ba52e1a023f51a0d
ms.sourcegitcommit: 8e7316bd4c4991de62ea485adca30065e5b86c67
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/17/2020
ms.locfileid: "94659519"
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a>Een op SLES of openSUSE gebaseerde virtuele machine voor Azure voorbereiden


In dit artikel wordt ervan uitgegaan dat u al een SUSE-of openSUSE Linux-besturings systeem hebt geïnstalleerd op een virtuele harde schijf. Er zijn meerdere hulpprogram ma's voor het maken van VHD-bestanden, zoals Hyper-V. Zie [de Hyper-V-functie installeren en een virtuele machine configureren](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh846766(v=ws.11))voor instructies.

## <a name="sles--opensuse-installation-notes"></a>SLES/openSUSE-installatie notities
* Zie ook [algemene Linux-installatie notities](create-upload-generic.md#general-linux-installation-notes) voor meer tips over het voorbereiden van Linux voor Azure.
* De VHDX-indeling wordt niet ondersteund in azure, alleen **vaste VHD**.  U kunt de schijf converteren naar VHD-indeling met behulp van Hyper-V-beheer of de cmdlet Convert-VHD.
* Bij de installatie van het Linux-systeem wordt aanbevolen om standaard partities te gebruiken in plaats van LVM (vaak de standaard instelling voor veel installaties). Hiermee wordt voor komen dat LVM naam strijdig is met gekloonde Vm's, met name als een besturingssysteem schijf ooit moet worden gekoppeld aan een andere virtuele machine voor het oplossen van problemen. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) kan worden gebruikt op gegevens schijven als dit de voor keur heeft.
* Configureer geen swap partitie op de besturingssysteem schijf. De Linux-agent kan worden geconfigureerd voor het maken van een wissel bestand op de tijdelijke bron schijf.  Meer informatie hierover vindt u in de volgende stappen.
* Alle Vhd's op Azure moeten een virtuele grootte hebben die is afgestemd op 1 MB. Wanneer u van een onbewerkte schijf naar VHD converteert, moet u ervoor zorgen dat de onbewerkte schijf grootte een meervoud van 1MB is vóór de conversie. Zie [installatie notities voor Linux](create-upload-generic.md#general-linux-installation-notes) voor meer informatie.

## <a name="use-suse-studio"></a>SUSE Studio gebruiken
[SuSE Studio](https://studioexpress.opensuse.org/) kan eenvoudig uw SLES-en openSUSE-installatie kopieën maken en beheren voor Azure en Hyper-V. Dit is de aanbevolen aanpak voor het aanpassen van uw eigen SLES-en openSUSE-installatie kopieën.

Als alternatief voor het maken van uw eigen VHD publiceert SUSE ook BYOS (uw eigen abonnementen meenemen) voor SLES op [VMDepot](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/04/using-and-contributing-vms-to-vm-depot.pdf).

## <a name="prepare-suse-linux-enterprise-server-for-azure"></a>SUSE Linux Enterprise Server voorbereiden voor Azure
1. Selecteer de virtuele machine in het middelste deel venster van Hyper-V-beheer.
2. Klik op **verbinding maken** om het venster voor de virtuele machine te openen.
3. Registreer uw SUSE Linux Enter prise-systeem zodat het updates kan downloaden en pakketten kan installeren.
4. Het systeem bijwerken met de meest recente patches:

    ```console
    # sudo zypper update
    ```
    
5. Azure Linux agent en Cloud-init installeren

    ```console
    # SUSEConnect -p sle-module-public-cloud/15.2/x86_64  (SLES 15 SP2)
    # sudo zypper install python-azure-agent
    # sudo zypper install cloud-init
    ```

6. Waagent & Cloud-init inschakelen om te starten bij het opstarten

    ```console
    # sudo chkconfig waagent on
    # systemctl enable cloud-init-local.service
    # systemctl enable cloud-init.service
    # systemctl enable cloud-config.service
    # systemctl enable cloud-final.service
    # systemctl daemon-reload
    # cloud-init clean
    ```

7. Waagent en Cloud-init-configuratie bijwerken

    ```console
    # sudo sed -i 's/ResourceDisk.Format=y/ResourceDisk.Format=n/g' /etc/waagent.conf
    # sudo sed -i 's/ResourceDisk.EnableSwap=y/ResourceDisk.EnableSwap=n/g' /etc/waagent.conf

    # sudo sh -c 'printf "datasource:\n  Azure:" > /etc/cloud/cloud.cfg.d/91-azure_datasource.cfg'
    # sudo sh -c 'printf "reporting:\n  logging:\n    type: log\n  telemetry:\n    type: hyperv" > /etc/cloud/cloud.cfg.d/10-azure-kvp.cfg'
    ```

8. Bewerk het/etc/default/grub-bestand om ervoor te zorgen dat console logboeken worden verzonden naar een seriële poort en werk vervolgens het hoofd configuratie bestand bij met grub2-mkconfig-o/boot/grub2/grub.cfg

    ```config-grub
    console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    ```
    Dit zorgt ervoor dat alle console berichten worden verzonden naar de eerste seriële poort, die ondersteuning voor Azure kan helpen bij het oplossen van problemen.
    
9. Zorg ervoor dat het bestand/etc/fstab-bestand verwijst naar de schijf met behulp van de UUID (per UUID)
         
10. Wijzig de udev-regels om te voor komen dat er statische regels voor de Ethernet-interface (s) worden gegenereerd. Deze regels kunnen problemen veroorzaken bij het klonen van een virtuele machine in Microsoft Azure of Hyper-V:

    ```console
    # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
    # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
    ```
   
11. Het is raadzaam om het bestand '/etc/sysconfig/network/DHCP ' te bewerken en de `DHCLIENT_SET_HOSTNAME` para meter te wijzigen in het volgende:

    ```config
    DHCLIENT_SET_HOSTNAME="no"
    ```

12. In/etc/sudoers kunt u de volgende regels uitchecken of verwijderen als deze bestaan:

    ```text
    Defaults targetpw   # ask for the password of the target user i.e. root
    ALL    ALL=(ALL) ALL   # WARNING! Only use this together with 'Defaults targetpw'!
    ```

13. Zorg ervoor dat de SSH-server is geïnstalleerd en geconfigureerd om te starten bij het opstarten. Dit is doorgaans de standaard instelling.

14. Maak geen wissel ruimte op de besturingssysteem schijf.
    
    De Azure Linux-agent kan tijdens het inrichten van Azure automatisch wissel ruimte configureren met de lokale bron schijf die aan de VM is gekoppeld. Houd er rekening mee dat de lokale bron schijf een *tijdelijke* schijf is en kan worden leeg gemaakt wanneer de inrichting van de virtuele machine wordt opheffen. Nadat u de Azure Linux-agent hebt geïnstalleerd (Zie de vorige stap), wijzigt u de volgende para meters in/etc/waagent.conf op de juiste manier:

    ```config-conf
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.EnableSwap=y
    ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
    ```

15. Voer de volgende opdrachten uit om de inrichting van de virtuele machine ongedaan te maken en deze voor te bereiden voor de inrichting van Azure:

    ```console
    # sudo waagent -force -deprovision
    # export HISTSIZE=0
    # logout
    ```
16. Klik op **actie-> afgesloten** in Hyper-V-beheer. Uw Linux-VHD is nu gereed om te worden geüpload naar Azure.

---
## <a name="prepare-opensuse-131"></a>OpenSUSE 13.1 + voorbereiden
1. Selecteer de virtuele machine in het middelste deel venster van Hyper-V-beheer.
2. Klik op **verbinding maken** om het venster voor de virtuele machine te openen.
3. Voer op de shell de opdracht uit `zypper lr` . Als met deze opdracht uitvoer wordt geretourneerd die vergelijkbaar is met de volgende, worden de opslag plaatsen op de verwachte manier geconfigureerd--er zijn geen aanpassingen nodig (Houd er rekening mee dat versie nummers kunnen variëren):

   | # | Alias                 | Naam                  | Ingeschakeld | Vernieuwen
   | - | :-------------------- | :-------------------- | :------ | :------
   | 1 | Cloud: Tools_13.1      | Cloud: Tools_13.1      | Ja     | Ja
   | 2 | openSUSE_13 openSUSE_13.1_OSS     | openSUSE_13 openSUSE_13.1_OSS     | Ja     | Ja
   | 3 | openSUSE_13 openSUSE_13.1_Updates | openSUSE_13 openSUSE_13.1_Updates | Ja     | Ja

    Als de opdracht ' geen opslag plaatsen gedefinieerd... ' retourneert gebruik vervolgens de volgende opdrachten om deze opslag plaatsen toe te voegen:

    ```console
    # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
    # sudo zypper ar -f https://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
    # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
    ```

    U kunt vervolgens controleren of de opslag plaatsen zijn toegevoegd door de opdracht `zypper lr` opnieuw uit te voeren. Als een van de relevante update opslagplaatsen niet is ingeschakeld, schakelt u deze in met de volgende opdracht:

    ```console
    # sudo zypper mr -e [NUMBER OF REPOSITORY]
    ```

4. Werk de kernel bij naar de meest recente beschik bare versie:

    ```console
    # sudo zypper up kernel-default
    ```

    Of om het systeem bij te werken met alle nieuwste patches:

    ```console
    # sudo zypper update
    ```

5. Installeer de Azure Linux-agent.

    ```console
    # sudo zypper install WALinuxAgent
    ```

6. Wijzig de kernel-opstart regel in de grub-configuratie zodat er aanvullende kernel-para meters voor Azure zijn. Om dit te doen, opent u "/boot/grub/menu.lst" in een tekst editor en zorgt u ervoor dat de standaard-kernel de volgende para meters bevat:

    ```config-grub
     console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    ```

   Dit zorgt ervoor dat alle console berichten worden verzonden naar de eerste seriële poort, die ondersteuning voor Azure kan helpen bij het oplossen van problemen. Verwijder bovendien de volgende para meters uit de opstart regel voor de kernel als deze bestaan:

    ```config-grub
     libata.atapi_enabled=0 reserve=0x1f0,0x8
    ```

7. Het is raadzaam om het bestand '/etc/sysconfig/network/DHCP ' te bewerken en de `DHCLIENT_SET_HOSTNAME` para meter te wijzigen in het volgende:

    ```config
     DHCLIENT_SET_HOSTNAME="no"
    ```

8. **Belang rijk:** In/etc/sudoers kunt u de volgende regels uitchecken of verwijderen als deze bestaan:

    ```text
    Defaults targetpw   # ask for the password of the target user i.e. root
    ALL    ALL=(ALL) ALL   # WARNING! Only use this together with 'Defaults targetpw'!
    ```

9. Zorg ervoor dat de SSH-server is geïnstalleerd en geconfigureerd om te starten bij het opstarten.  Dit is doorgaans de standaard instelling.
10. Maak geen wissel ruimte op de besturingssysteem schijf.

    De Azure Linux-agent kan tijdens het inrichten van Azure automatisch wissel ruimte configureren met de lokale bron schijf die aan de VM is gekoppeld. Houd er rekening mee dat de lokale bron schijf een *tijdelijke* schijf is en kan worden leeg gemaakt wanneer de inrichting van de virtuele machine wordt opheffen. Nadat u de Azure Linux-agent hebt geïnstalleerd (Zie de vorige stap), wijzigt u de volgende para meters in/etc/waagent.conf op de juiste manier:

    ```config-conf
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.EnableSwap=y
    ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
    ```

11. Voer de volgende opdrachten uit om de inrichting van de virtuele machine ongedaan te maken en deze voor te bereiden voor de inrichting van Azure:

    ```console
    # sudo waagent -force -deprovision
    # export HISTSIZE=0
    # logout
    ```

12. Zorg ervoor dat de Azure Linux-agent wordt uitgevoerd bij het opstarten:

    ```console
    # sudo systemctl enable waagent.service
    ```

13. Klik op **actie-> afgesloten** in Hyper-V-beheer. Uw Linux-VHD is nu gereed om te worden geüpload naar Azure.

## <a name="next-steps"></a>Volgende stappen
U kunt nu uw SUSE Linux-virtuele harde schijf gebruiken om nieuwe virtuele machines te maken in Azure. Zie [een virtuele Linux-machine maken op basis van een aangepaste schijf](upload-vhd.md#option-1-upload-a-vhd)als dit de eerste keer is dat u het VHD-bestand naar Azure uploadt.
