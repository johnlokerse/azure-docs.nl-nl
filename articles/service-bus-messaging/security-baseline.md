---
title: Azure-beveiligings basislijn voor Service Bus
description: De Service Bus Security Baseline voorziet in procedure richtlijnen en resources voor het implementeren van de beveiligings aanbevelingen die zijn opgegeven in de Azure Security-Bench Mark.
author: msmbaldwin
ms.service: service-bus-messaging
ms.topic: conceptual
ms.date: 09/25/2020
ms.author: mbaldwin
ms.custom: subject-security-benchmark
ms.openlocfilehash: a6d4e7f4ca7288b36f6801b9ddb362b7e936862d
ms.sourcegitcommit: 0a9df8ec14ab332d939b49f7b72dea217c8b3e1e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94843618"
---
# <a name="azure-security-baseline-for-service-bus"></a>Azure-beveiligings basislijn voor Service Bus

De Azure-beveiligings basislijn voor Service Bus bevat aanbevelingen waarmee u de beveiligings postuur van uw implementatie kunt verbeteren. De basis lijn voor deze service wordt opgehaald uit de [Azure Security Bench Mark-versie 1,0](../security/benchmarks/overview-v1.md), die aanbevelingen biedt over hoe u uw cloud oplossingen kunt beveiligen in azure met onze richt lijnen voor best practices. Zie [overzicht van Azure Security-basis lijnen](../security/benchmarks/security-baselines-overview.md)voor meer informatie.

Als u wilt zien hoe Service Bus volledig is toegewezen aan de beveiligings benchmark van Azure, raadpleegt u het [volledige service bus beveiligings basislijn toewijzings bestand](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines).

## <a name="network-security"></a>Netwerkbeveiliging

*Zie [Azure Security Bench Mark: Network Security](../security/benchmarks/security-control-network-security.md)(Engelstalig) voor meer informatie.*

### <a name="11-protect-azure-resources-within-virtual-networks"></a>1,1: Azure-resources in virtuele netwerken beveiligen 

**Hulp**: de integratie van service bus met de Azure Private Link-service biedt beveiligde persoonlijke toegang tot berichten mogelijkheden van werk belastingen, zoals virtuele machines die zijn gebonden aan virtuele netwerken. Maak een verbinding voor een persoonlijk eind punt met uw Service Bus-naam ruimte. Het persoonlijke eind punt maakt gebruik van een privé-IP-adres van uw virtuele netwerk, waardoor de service in het virtuele netwerk effectief wordt. Al het verkeer naar de service kan worden doorgestuurd via dat persoonlijke eind punt, zodat er geen gateways, NAT-apparaten, ExpressRoute of VPN-verbindingen of open bare IP-adressen nodig zijn.

U kunt uw Azure Service Bus naam ruimte ook beveiligen door gebruik te maken van firewalls. Azure Service Bus ondersteunt toegangs beheer op basis van IP voor binnenkomende firewall ondersteuning. U kunt Firewall regels instellen met behulp van de Azure Portal, Azure Resource Manager sjablonen of via de Azure CLI of Azure PowerShell.

- [Toegang tot Azure Service Bus naam ruimten toestaan via persoonlijke eind punten](private-link-service.md)

- [Toegang tot Azure Service Bus naam ruimte van specifieke IP-adressen of bereiken toestaan](service-bus-ip-filtering.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="12-monitor-and-log-the-configuration-and-traffic-of-virtual-networks-subnets-and-network-interfaces"></a>1,2: de configuratie en het verkeer van virtuele netwerken, subnetten en netwerk interfaces bewaken en vastleggen

**Richt lijnen**: als u virtuele Azure-machines gebruikt om toegang te krijgen tot uw service bus-entiteiten, schakelt u de stroom logboeken voor netwerk beveiligings groepen (NSG) in en verzendt u logboeken naar een opslag account voor verkeers controle. U kunt ook NSG-stroom logboeken naar een Log Analytics-werk ruimte verzenden en Traffic Analytics gebruiken om inzicht te krijgen in de verkeers stroom in uw Azure-Cloud. Enkele voor delen van Traffic Analytics zijn de mogelijkheid om netwerk activiteiten te visualiseren en HOTS pots te identificeren, beveiligings dreigingen te identificeren, verkeers patronen te begrijpen en netwerk configuraties te lokaliseren. 

Gebruik Azure Security Center en volg aanbevelingen voor netwerk beveiliging om uw Service Bus resources in azure te beveiligen.

- [NSG-stroom logboeken inschakelen](../network-watcher/network-watcher-nsg-flow-logging-portal.md)

- [Traffic Analytics inschakelen en gebruiken](../network-watcher/traffic-analytics.md)

- [Network Watcher inschakelen](../network-watcher/network-watcher-create.md)

- [Informatie over netwerk beveiliging die wordt verschaft door Azure Security Center](../security-center/security-center-network-recommendations.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="14-deny-communications-with-known-malicious-ip-addresses"></a>1,4: communicatie met bekende schadelijke IP-adressen weigeren

**Hulp**: Schakel DDoS Protection standaard in voor de virtuele netwerken die zijn gekoppeld aan uw service bus-naam ruimten om te beschermen tegen gedistribueerde Denial-of-service-aanvallen (DDoS). Gebruik Azure Security Center geïntegreerde bedreigings informatie om communicatie met bekende of ongebruikte Internet-IP-adressen te weigeren.

- [DDoS-beveiliging configureren](../virtual-network/manage-ddos-protection.md)

- [Geïntegreerde bedreigings informatie Azure Security Center](../security-center/azure-defender.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="15-record-network-packets"></a>1,5: netwerk pakketten opnemen

**Richt lijnen**: als u virtuele Azure-machines gebruikt om toegang te krijgen tot uw service bus-entiteiten, kunt u Network Watcher pakket opname gebruiken om afwijkende activiteiten te onderzoeken.

- [Network Watcher inschakelen](../network-watcher/network-watcher-create.md)

**Azure Security Center bewaking**: momenteel niet beschikbaar

**Verantwoordelijkheid**: klant

### <a name="16-deploy-network-based-intrusion-detectionintrusion-prevention-systems-idsips"></a>1,6: op netwerk gebaseerde inbreuk detectie/indringings systemen (ID'S/IP-adressen) implementeren

**Richt lijnen**: als u virtuele Azure-machines gebruikt om toegang te krijgen tot uw service bus-entiteiten, selecteert u een aanbieding in de Azure Marketplace die ondersteuning biedt voor ID'S/IP-adressen met Payload-inspectie mogelijkheden. Als inbraak detectie en/of preventie op basis van Payload-inspectie niet vereist is voor uw organisatie, kunt u de ingebouwde firewall functie van Azure Service Bus gebruiken. U kunt de toegang tot uw Service Bus-naam ruimte beperken voor een beperkt bereik van IP-adressen of een specifiek IP-adres met behulp van firewall regels.

- [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/?term=Firewall)

- [Een firewall regel toevoegen in Service Bus naam ruimten voor een opgegeven IP-adres](service-bus-ip-filtering.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="18-minimize-complexity-and-administrative-overhead-of-network-security-rules"></a>1,8: de complexiteit en administratieve overhead van netwerk beveiligings regels minimaliseren

**Hulp**: gebruik Virtual Network Service Tags om netwerk toegangs beheer te definiëren voor netwerk beveiligings groepen of Azure firewall die verkeer van en naar Service Bus-resources filteren. U kunt servicetags gebruiken in plaats van specifieke IP-adressen wanneer u beveiligingsregels maakt. Door de naam van de service label (bijvoorbeeld ServiceBus) op te geven in het juiste bron-of doel veld van een regel, kunt u het verkeer voor de bijbehorende service toestaan of weigeren. Micro soft beheert de adres voorvoegsels die zijn opgenomen in het servicetag van de service en werkt de servicetag automatisch bij met gewijzigde adressen. 

- [Service Tags begrijpen en gebruiken](../virtual-network/service-tags-overview.md)

**Azure Security Center bewaking**: momenteel niet beschikbaar

**Verantwoordelijkheid**: klant

### <a name="19-maintain-standard-security-configurations-for-network-devices"></a>1,9: standaard beveiligings configuraties voor netwerk apparaten onderhouden

**Hulp**: Definieer en implementeer standaard beveiligings configuraties voor netwerk bronnen die zijn gekoppeld aan uw Azure service bus-naam ruimten met Azure Policy. Gebruik Azure Policy aliassen in de naam ruimten ' micro soft. ServiceBus ' en ' micro soft. Network ' om aangepaste beleids regels te maken om de netwerk configuratie van uw Service Bus naam ruimten te controleren of af te dwingen. U kunt ook gebruik maken van ingebouwde beleids definities die betrekking hebben op Azure Service Bus, zoals:

- Service Bus moet gebruikmaken van een service-eindpunt voor een virtueel netwerk
- Diagnostische logboeken in Service Bus moeten zijn ingeschakeld

U kunt ook aangepaste beleids definities maken als de ingebouwde definities niet voldoen aan de behoeften van uw organisatie.

- [Azure Policy configureren en beheren](../governance/policy/tutorials/create-and-manage.md)

- [Ingebouwd beleid voor Azure voor Service Bus naam ruimte](./policy-reference.md#azure-service-bus-messaging)

- [Voor beelden Azure Policy voor netwerken](../governance/policy/samples/built-in-policies.md#network)

- [Een Azure Blueprint maken](../governance/blueprints/create-blueprint-portal.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="110-document-traffic-configuration-rules"></a>1,10: configuratie regels voor het document verkeer

**Hulp**: Labels gebruiken voor virtuele netwerken en andere bronnen die betrekking hebben op netwerk beveiliging en verkeers stroom die zijn gekoppeld aan uw service bus-naam ruimten. Gebruik voor afzonderlijke regels voor de netwerk beveiligings groep het veld Beschrijving om de bedrijfs behoeften, duur en andere beschrijvende gegevens op te geven voor regels die verkeer van of naar een netwerk dat is gekoppeld aan uw Service Bus-naam ruimten. 

Gebruik een van de ingebouwde Azure-beleids definities die betrekking hebben op labelen, zoals ' vereist label en de waarde ', om ervoor te zorgen dat alle resources met tags worden gemaakt en u op de hoogte moet zijn van bestaande niet-gelabelde resources. 

U kunt Azure PowerShell of Azure CLI gebruiken om op basis van hun labels acties op resources te zoeken of uit te voeren. 

- [Tags maken en gebruiken](../azure-resource-manager/management/tag-resources.md) 

- [Een Virtual Network maken](../virtual-network/quick-create-portal.md) 

- [Een NSG maken met een beveiligings configuratie](../virtual-network/tutorial-filter-network-traffic.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="111-use-automated-tools-to-monitor-network-resource-configurations-and-detect-changes"></a>1,11: gebruik automatische hulpprogram ma's om netwerk bron configuraties te bewaken en wijzigingen te detecteren

**Hulp**: Azure-activiteiten logboek gebruiken om netwerk resource configuraties te bewaken en wijzigingen te detecteren voor netwerk bronnen die betrekking hebben op Azure service bus. Maak waarschuwingen in Azure Monitor die worden geactiveerd wanneer er wijzigingen in kritieke netwerk bronnen plaatsvinden.

- [Activiteiten logboek gebeurtenissen van Azure weer geven en ophalen](../azure-monitor/platform/activity-log.md#view-the-activity-log)

- [Waarschuwingen maken in Azure Monitor](../azure-monitor/platform/alerts-activity-log.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

## <a name="logging-and-monitoring"></a>Logboekregistratie en bewaking

*Zie [Azure Security Bench Mark: Logging and monitoring](../security/benchmarks/security-control-logging-monitoring.md)(Engelstalig) voor meer informatie.*

### <a name="22-configure-central-security-log-management"></a>2,2: Centraal beveiligings logboek beheer configureren

**Hulp**: opname logboeken via Azure monitor voor het verzamelen van beveiligings gegevens die door service bus resources zijn gegenereerd. Gebruik in Azure Monitor Log Analytics-werk ruimten voor het opvragen en uitvoeren van analyses, Configureer Azure Storage accounts voor lange termijn-of archief opslag. U kunt ook logboeken met betrekking tot Service Bus configureren om te worden verzonden naar Azure Sentinel of een SIEM van derden.

- [Diagnostische instellingen voor Azure Service Bus configureren](service-bus-diagnostic-logs.md)

- [Informatie over Azure-activiteiten logboek](../azure-monitor/platform/platform-logs-overview.md)

- [Azure-Sentinel onboarden](../sentinel/quickstart-onboard.md) 

- [Aan de slag met Azure Monitor en integratie van SIEM van derden](https://azure.microsoft.com/blog/use-azure-monitor-to-integrate-with-siem-tools/)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="23-enable-audit-logging-for-azure-resources"></a>2,3: controle logboek registratie inschakelen voor Azure-resources

**Hulp**: Diagnostische instellingen inschakelen voor uw Azure service bus naam ruimte. Azure Service Bus ondersteunt momenteel activiteiten en operationele of diagnostische Logboeken. Activiteiten logboeken bevatten informatie over bewerkingen die worden uitgevoerd voor een taak. Diagnostische logboeken bieden uitgebreide informatie over bewerkingen en acties die worden uitgevoerd op uw naam ruimte met behulp van API of via beheer-clients die gebruikmaken van de taal-SDK. In deze logboeken wordt het bewerkings type vastgelegd, inclusief het maken van de wachtrij, de gebruikte resources en de status van de bewerking.

- [Diagnostische instellingen inschakelen voor Azure Service Bus](service-bus-diagnostic-logs.md)

- [Diagnostische instellingen voor Azure-activiteiten logboek inschakelen](../azure-monitor/platform/activity-log.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="25-configure-security-log-storage-retention"></a>2,5: Bewaar beveiliging van het beveiligings logboek configureren

**Richt lijnen**: stel binnen Azure monitor uw Bewaar periode voor log Analytics werk ruimte in volgens de nalevings regels van uw organisatie om service bus-gerelateerde incidenten vast te leggen en te controleren.

- [Para meters voor het bewaren van Logboeken instellen voor Log Analytics-werk ruimten](../azure-monitor/platform/manage-cost-storage.md#change-the-data-retention-period)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="26-monitor-and-review-logs"></a>2,6: Logboeken bewaken en controleren

**Richt lijnen**: Logboeken analyseren en bewaken voor afwijkend gedrag en regel matige resultaten controleren met betrekking tot uw service bus entiteiten. Gebruik Azure Monitor om logboeken te controleren en query's uit te voeren op logboek gegevens met betrekking tot Service Bus.

- [Voor meer informatie over de Log Analytics-werk ruimte](../azure-monitor/log-query/get-started-portal.md)

- [Aangepaste query's uitvoeren in Azure Monitor](../azure-monitor/log-query/get-started-queries.md)

- [Azure-Sentinel onboarden](../sentinel/quickstart-onboard.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="27-enable-alerts-for-anomalous-activities"></a>2,7: waarschuwingen inschakelen voor afwijkende activiteiten

**Hulp**: gebruik Azure Security Center met log Analytics werk ruimte voor bewaking en waarschuwingen over afwijkende activiteiten die in beveiligings logboeken en gebeurtenissen zijn gevonden. U kunt ook gegevens naar Azure-Sentinel inschakelen en op het bord zetten.

- [Azure-Sentinel onboarden](../sentinel/quickstart-onboard.md)

- [Waarschuwingen beheren in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md)

- [Een waarschuwing over logboek gegevens van log Analytics](../azure-monitor/learn/tutorial-response.md)

**Azure Security Center bewaking**: momenteel niet beschikbaar

**Verantwoordelijkheid**: klant

## <a name="identity-and-access-control"></a>Identiteits- en toegangsbeheer

*Zie [Azure Security Bench Mark: identiteits-en toegangs beheer](../security/benchmarks/security-control-identity-access-control.md)voor meer informatie.*

### <a name="31-maintain-an-inventory-of-administrative-accounts"></a>3,1: een inventaris van beheerders accounts onderhouden

**Richt lijnen**: met Azure op rollen gebaseerd toegangs beheer (Azure RBAC) kunt u de toegang tot Azure-resources beheren via roltoewijzingen. U kunt deze rollen toewijzen aan gebruikers, groeperingen van service-principals en beheerde identiteiten. Er zijn vooraf gedefinieerde ingebouwde rollen voor Service Bus. deze rollen kunnen worden geïnventariseerd of worden opgevraagd via hulpprogram ma's als Azure CLI, Azure PowerShell of de Azure Portal.

- [Ingebouwde rollen voor Azure Service Bus](authenticate-application.md#azure-built-in-roles-for-azure-service-bus)

- [Een directory-rol verkrijgen in azure AD met Power shell](/powershell/module/azuread/get-azureaddirectoryrole?view=azureadps-2.0) 

- [Leden van een directory-rol in azure AD ophalen met Power shell](/powershell/module/azuread/get-azureaddirectoryrolemember?view=azureadps-2.0)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="32-change-default-passwords-where-applicable"></a>3,2: standaard wachtwoorden wijzigen indien van toepassing

**Hulp**: beheer van toegang tot service bus wordt beheerd via Azure Active Directory (Azure AD). Azure AD heeft niet het concept van standaard wachtwoorden.

De toegang tot het gegevens vlak tot Service Bus wordt beheerd via Azure AD met behulp van beheerde identiteiten, App-registraties of Shared Access signatures. Shared Access signatures worden gebruikt door de clients die verbinding maken met uw Service Bus naam ruimte en kunnen op elk gewenst moment opnieuw worden gegenereerd.

- [Informatie over gedeelde toegangs handtekeningen voor Service Bus](service-bus-sas.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="33-use-dedicated-administrative-accounts"></a>3,3: speciale beheerders accounts gebruiken

**Richt lijnen**: Maak standaard procedures voor het gebruik van specifieke beheerders accounts. Gebruik Azure Security Center identiteits-en toegangs beheer om het aantal beheerders accounts te bewaken.

Daarnaast kunt u aanbevelingen van Azure Security Center of ingebouwde Azure-beleids regels gebruiken om u te helpen bij het bijhouden van specifieke beheerders accounts, zoals:

- Er moet meer dan één eigenaar zijn toegewezen aan uw abonnement
- Afgeschafte accounts met eigenaarsmachtigingen moeten worden verwijderd uit uw abonnement
- Externe accounts met eigenaarsmachtigingen moeten worden verwijderd uit uw abonnement

U kunt ook aangepaste beleids definities maken als de ingebouwde definities niet voldoen aan de behoeften van uw organisatie.

- [Azure Security Center gebruiken om identiteit en toegang te bewaken](../security-center/security-center-identity-access.md)

- [Azure Policy gebruiken](../governance/policy/tutorials/create-and-manage.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="34-use-azure-active-directory-single-sign-on-sso"></a>3,4: gebruik Azure Active Directory eenmalige aanmelding (SSO)

**Hulp**: Microsoft Azure biedt geïntegreerd beheer van toegangs beheer voor bronnen en toepassingen op basis van Azure Active Directory (Azure AD). Een belang rijk voor deel van het gebruik van Azure AD met Azure Service Bus is dat u uw referenties niet meer hoeft op te slaan in de code. In plaats daarvan kunt u een OAuth 2,0-toegangs token aanvragen bij het micro soft Identity-platform. De resource naam voor het aanvragen van een token is https://azure.microsoft.com/services/service-bus/ . Azure AD verifieert de beveiligingsprincipal (een gebruiker, groep of Service-Principal) die de toepassing uitvoert. Als de verificatie slaagt, retourneert Azure AD een toegangs token voor de toepassing en kan de toepassing vervolgens het toegangs token gebruiken om de aanvraag voor het Azure Service Bus van resources te autoriseren.

- [Een toepassing verifiëren met Azure AD om toegang te krijgen tot Service Bus bronnen](authenticate-application.md)

- [Informatie over eenmalige aanmelding met Azure AD](../active-directory/manage-apps/what-is-single-sign-on.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="35-use-multi-factor-authentication-for-all-azure-active-directory-based-access"></a>3,5: multi-factor Authentication gebruiken voor alle op Azure Active Directory gebaseerde toegang

**Hulp**: schakel Azure Active Directory multi-factor Authentication (MFA) in en volg de aanbevelingen voor Azure Security Center identiteits-en toegangs beheer om uw resources met Service bus te beveiligen.

- [MFA inschakelen in azure](../active-directory/authentication/howto-mfa-getstarted.md)

- [Identiteit en toegang bewaken in Azure Security Center](../security-center/security-center-identity-access.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="36-use-secure-azure-managed-workstations-for-administrative-tasks"></a>3,6: beveiligde, door Azure beheerde werk stations gebruiken voor beheer taken

**Hulp**: gebruik paw (privileged Access workstations) met multi-factor Authentication (MFA) die zijn geconfigureerd voor aanmelding bij en configureren van service bus-ingeschakelde resources.

- [Meer informatie over privileged Access workstations](/windows-server/identity/securing-privileged-access/privileged-access-workstations)

- [MFA inschakelen in azure](../active-directory/authentication/howto-mfa-getstarted.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="37-log-and-alert-on-suspicious-activities-from-administrative-accounts"></a>3,7: Logboeken en waarschuwingen voor verdachte activiteiten van beheerders accounts

**Hulp**: gebruik Azure Active Directory beveiligings rapporten en-bewaking om te detecteren wanneer verdachte of onveilige activiteiten in de omgeving worden uitgevoerd. Gebruik Azure Security Center om identiteits-en toegangs activiteiten te bewaken.

- [Azure AD-gebruikers identificeren die zijn gemarkeerd voor Risk ante activiteiten](../active-directory/identity-protection/overview-identity-protection.md)

- [Identiteits-en toegangs activiteiten van gebruikers controleren in Azure Security Center](../security-center/security-center-identity-access.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="38-manage-azure-resources-from-only-approved-locations"></a>3,8: Azure-resources alleen beheren vanaf goedgekeurde locaties

**Richt lijnen**: gebruik Azure AD benoemde locaties om alleen toegang toe te staan vanuit specifieke logische groepen met IP-adresbereiken of landen/regio's. 

- [De benoemde locaties van Azure AD configureren](../active-directory/reports-monitoring/quickstart-configure-named-locations.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="39-use-azure-active-directory"></a>3,9: Azure Active Directory gebruiken

**Hulp**: gebruik Azure Active Directory (AD) als centraal verificatie-en autorisatie systeem voor Azure-resources, zoals service bus. Hiermee kunnen op rollen gebaseerd toegangs beheer (Azure RBAC) van Azure worden uitgevoerd voor beheer gevoelige bronnen.

- [Een Azure AD-exemplaar maken en configureren](../active-directory/fundamentals/active-directory-access-create-new-tenant.md)

- [Toegang tot Service Bus resources autoriseren met behulp van Azure Active Directory](authenticate-application.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="310-regularly-review-and-reconcile-user-access"></a>3,10: regel matig gebruikers toegang controleren en afstemmen

**Hulp**: Azure Active Directory (Azure AD) bevat logboeken waarmee u verouderde accounts kunt detecteren. Daarnaast kunt u Azure Identity Access revisies gebruiken om groepslid maatschappen en de toegang tot bedrijfs toepassingen en roltoewijzingen op efficiënte wijze te beheren. Gebruikers toegang kan regel matig worden gecontroleerd om ervoor te zorgen dat alleen de juiste gebruikers toegang hebben.

U kunt de gedeelde toegangs handtekening van de Service Bus naam ruimte echter op een andere regel laten draaien.

- [Meer informatie over Azure AD-rapportage](../active-directory/reports-monitoring/index.yml)

- [Beoordelingen over Azure Identity Access gebruiken](../active-directory/governance/access-reviews-overview.md)

- [Informatie over gedeelde toegangs handtekeningen voor Service Bus naam ruimte](service-bus-sas.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="311-monitor-attempts-to-access-deactivated-credentials"></a>3,11: controle pogingen om toegang te krijgen tot gedeactiveerde referenties

**Richt lijnen**: u hebt toegang tot Azure Active Directory (Azure AD) aanmeldings activiteit, controle en risico logboek bronnen, waarmee u kunt integreren met Azure Sentinel of een Siem-hulp programma van derden.

U kunt dit proces stroom lijnen door Diagnostische instellingen voor Azure AD-gebruikers accounts te maken en de audit logboeken en aanmeldings logboeken te verzenden naar een Log Analytics-werk ruimte. In Azure Monitor kunt u vervolgens de gewenste logboek waarschuwingen configureren voor bepaalde acties die in de logboeken optreden.

- [Azure-activiteiten logboeken integreren in Azure Monitor](../active-directory/reports-monitoring/howto-integrate-activity-logs-with-log-analytics.md)

- [Toegang tot Service Bus resources autoriseren met behulp van Azure Active Directory](authenticate-application.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="312-alert-on-account-sign-in-behavior-deviation"></a>3,12: waarschuwing voor de afwijking van het aanmeldings gedrag van het account

**Hulp**: gebruik de functies voor identiteits beveiliging en risico detectie van Azure Active Directory om automatische antwoorden te configureren op gedetecteerde verdachte acties die betrekking hebben op uw service bus-resources. Schakel automatische antwoorden via Azure Sentinel in om de beveiligings reacties van uw organisatie te implementeren.

- [Risk ante aanmeldingen voor Azure AD weer geven](../active-directory/identity-protection/overview-identity-protection.md)

- [Risico beleid voor identiteits beveiliging configureren en inschakelen](../active-directory/identity-protection/howto-identity-protection-configure-risk-policies.md)

- [Azure-Sentinel onboarden](../sentinel/quickstart-onboard.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="313-provide-microsoft-with-access-to-relevant-customer-data-during-support-scenarios"></a>3,13: micro soft biedt toegang tot relevante klant gegevens tijdens ondersteunings scenario's

**Hulp**: momenteel niet beschikbaar; Klanten-lockbox wordt nog niet ondersteund voor Service Bus.

- [Lijst met door Klanten-lockbox ondersteunde services](../security/fundamentals/customer-lockbox-overview.md#supported-services-and-scenarios-in-general-availability)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

## <a name="data-protection"></a>Gegevensbescherming

*Zie [Azure Security Bench Mark: Data Protection](../security/benchmarks/security-control-data-protection.md)voor meer informatie.*

### <a name="41-maintain-an-inventory-of-sensitive-information"></a>4,1: een inventaris van gevoelige informatie onderhouden

**Hulp**: Gebruik labels op resources die betrekking hebben op uw service bus voor het bijhouden van Azure-resources die gevoelige informatie opslaan of verwerken.

- [Tags maken en gebruiken](../azure-resource-manager/management/tag-resources.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="42-isolate-systems-storing-or-processing-sensitive-information"></a>4,2: systemen isoleren die gevoelige informatie opslaan of verwerken

**Richt lijnen**: afzonderlijke abonnementen en beheer groepen implementeren voor ontwikkeling, testen en productie. Service Bus naam ruimten moeten worden gescheiden door virtuele netwerken met persoonlijke eind punten die op de juiste wijze zijn geconfigureerd en gelabeld.

- [Aanvullende Azure-abonnementen maken](../cost-management-billing/manage/create-subscription.md)

- [Beheergroepen maken](../governance/management-groups/create-management-group-portal.md)

- [Tags maken en gebruiken](../azure-resource-manager/management/tag-resources.md)

- [Een Virtual Network maken](../virtual-network/quick-create-portal.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="43-monitor-and-block-unauthorized-transfer-of-sensitive-information"></a>4,3: niet-geautoriseerde overdracht van gevoelige gegevens controleren en blok keren

**Richt lijnen**: wanneer u virtuele machines gebruikt om toegang te krijgen tot uw service bus entiteiten, maakt u gebruik van virtuele netwerken, persoonlijke eind punten, service bus firewall, netwerk beveiligings groepen en service tags om de kans op gegevens exfiltration te beperken.

Micro soft beheert de onderliggende infra structuur voor Azure Service Bus en heeft strikte controles geïmplementeerd om verlies of bloot stelling van klant gegevens te voor komen.

- [IP-firewall regels voor Azure Service Bus naam ruimten configureren](service-bus-ip-filtering.md)

- [Toegang tot Azure Service Bus naam ruimte vanuit specifieke virtuele netwerken toestaan](private-link-service.md)

- [Toegang tot Azure Service Bus naam ruimten toestaan via persoonlijke eind punten](private-link-service.md)

- [Meer informatie over netwerk beveiligings groepen en service Tags](../virtual-network/network-security-groups-overview.md)

- [Informatie over beveiliging van klanten in azure](../security/fundamentals/protection-customer-data.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: gedeeld

### <a name="44-encrypt-all-sensitive-information-in-transit"></a>4,4: alle gevoelige gegevens in de overdracht versleutelen

**Hulp**: Azure service bus worden standaard TLS-versleutelde communicatie afgedwongen. TLS-versies 1,0, 1,1 en 1,2 worden momenteel ondersteund. TLS 1,0 en 1,1 bevinden zich echter op een pad naar de hele industrie, dus gebruik waar mogelijk TLS 1,2 of nieuwer.

- [Zie netwerk beveiliging voor informatie over de beveiligings functies van Service Bus](network-security.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: gedeeld

### <a name="45-use-an-active-discovery-tool-to-identify-sensitive-data"></a>4,5: een actief detectie hulpprogramma gebruiken om gevoelige gegevens te identificeren

**Hulp**: de functies gegevens identificatie, classificatie en verlies preventie zijn nog niet beschikbaar voor Azure service bus. Implementeer oplossingen van derden, indien nodig voor nalevings doeleinden.

Voor het onderliggende platform dat door micro soft wordt beheerd, behandelt micro soft alle inhoud van de klant als gevoelig en gaat u naar een fantastische lengte om te beschermen tegen verlies en bloot stelling van klant gegevens. Om ervoor te zorgen dat klant gegevens binnen Azure veilig blijven, heeft micro soft een reeks robuuste besturings elementen en mogelijkheden voor gegevens bescherming geïmplementeerd en onderhouden.

- [Informatie over beveiliging van klanten in azure](../security/fundamentals/protection-customer-data.md)

**Azure Security Center bewaking**: momenteel niet beschikbaar

**Verantwoordelijkheid**: gedeeld

### <a name="46-use-role-based-access-control-to-control-access-to-resources"></a>4,6: op rollen gebaseerd toegangs beheer gebruiken voor het beheren van de toegang tot bronnen

**Hulp**: Azure service bus ondersteunt het gebruik van Azure Active Directory (Azure AD) voor het machtigen van aanvragen voor het service bus van entiteiten. Met Azure AD kunt u Azure RBAC (op rollen gebaseerd toegangs beheer) gebruiken om machtigingen te verlenen aan een beveiligingsprincipal, die een gebruiker of een service-principal van de toepassing is.

- [Meer informatie over Azure RBAC en de beschik bare rollen voor Azure Service Bus](authenticate-application.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="48-encrypt-sensitive-information-at-rest"></a>4,8: gevoelige informatie op rest versleutelen

**Hulp**: Azure service bus ondersteunt de mogelijkheid om gegevens in rust te versleutelen met door micro soft beheerde sleutels of door de klant beheerde sleutels. Met deze functie kunt u toegang tot de door de klant beheerde sleutels maken, draaien, uitschakelen en intrekken die worden gebruikt voor het versleutelen van Azure Service Bus gegevens in rust.

- [Door de klant beheerde sleutels voor het versleutelen van Azure Service Bus configureren](configure-customer-managed-key.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="49-log-and-alert-on-changes-to-critical-azure-resources"></a>4,9: wijzigingen in essentiële Azure-resources vastleggen en waarschuwen

**Hulp**: gebruik Azure monitor met het Azure-activiteiten logboek om waarschuwingen te maken wanneer wijzigingen worden aangebracht in productie-exemplaren van Azure service bus en andere essentiële of gerelateerde resources.

- [Waarschuwingen maken voor gebeurtenissen in het Azure-activiteiten logboek](../azure-monitor/platform/alerts-activity-log.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

## <a name="inventory-and-asset-management"></a>Inventarisatie en asset-management

*Zie [Azure Security Bench Mark: Inventory and Asset Management](../security/benchmarks/security-control-inventory-asset-management.md)voor meer informatie.*

### <a name="61-use-automated-asset-discovery-solution"></a>6,1: automatische Asset-detectie oplossing gebruiken

**Richt lijnen**: gebruik Azure resource Graph om alle resources (inclusief Azure service bus naam ruimten) binnen uw abonnementen te doorzoeken en te detecteren. Zorg ervoor dat u de juiste machtigingen (lezen) hebt in uw Tenant en dat u alle Azure-abonnementen kunt inventariseren, evenals de resources in uw abonnementen.

- [Query's maken met Azure resource Graph](../governance/resource-graph/first-query-portal.md)

- [Uw Azure-abonnementen weer geven](/powershell/module/az.accounts/get-azsubscription?view=azps-3.0.0)

- [Meer informatie over Azure RBAC](../role-based-access-control/overview.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="62-maintain-asset-metadata"></a>6,2: meta gegevens van activa onderhouden

**Richt lijnen**: Tags Toep assen op Azure-resources die meta gegevens geven om ze logisch in een taxonomie te organiseren.

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="63-delete-unauthorized-azure-resources"></a>6,3: niet-geautoriseerde Azure-resources verwijderen

**Richt lijnen**: Gebruik labels, beheer groepen en afzonderlijke abonnementen, waar nodig, om Azure service bus naam ruimten en gerelateerde resources te organiseren en bij te houden. Sluit de inventaris regel matig af en zorg ervoor dat niet-geautoriseerde resources tijdig worden verwijderd uit het abonnement.

- [Aanvullende Azure-abonnementen maken](../cost-management-billing/manage/create-subscription.md)

- [Beheergroepen maken](../governance/management-groups/create-management-group-portal.md)

- [Tags maken en gebruiken](../azure-resource-manager/management/tag-resources.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="64-define-and-maintain-inventory-of-approved-azure-resources"></a>6,4: de inventaris van goedgekeurde Azure-resources definiëren en onderhouden

**Richt lijnen**: Maak een inventaris van goedgekeurde Azure-resources en goedgekeurde software voor reken resources conform uw organisatie behoeften.

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="65-monitor-for-unapproved-azure-resources"></a>6,5: monitor voor niet-goedgekeurde Azure-resources

**Hulp: gebruik** Azure Policy om beperkingen toe te voegen voor het type resources dat kan worden gemaakt in klant abonnementen met behulp van de volgende ingebouwde beleids definities:

- Niet toegestane resourcetypen

- Toegestane brontypen

Daarnaast kunt u met Azure resource Graph bronnen in de abonnementen opvragen en detecteren.

- [Azure Policy configureren en beheren](../governance/policy/tutorials/create-and-manage.md)

- [Query's maken met Azure Graph](../governance/resource-graph/first-query-portal.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="69-use-only-approved-azure-services"></a>6,9: alleen goedgekeurde Azure-Services gebruiken

**Hulp: gebruik** Azure Policy om beperkingen toe te voegen voor het type resources dat kan worden gemaakt in klant abonnementen met behulp van de volgende ingebouwde beleids definities:

- Niet toegestane resourcetypen
- Toegestane brontypen

U kunt ook aangepaste beleids definities maken als de ingebouwde definities niet voldoen aan de behoeften van uw organisatie.

- [Azure Policy configureren en beheren](../governance/policy/tutorials/create-and-manage.md)

- [Een specifiek resource type weigeren met Azure Policy](../governance/policy/samples/index.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="611-limit-users-ability-to-interact-with-azure-resource-manager"></a>6,11: de mogelijkheid van gebruikers om te communiceren met Azure Resource Manager beperken

**Hulp** bij het configureren van voorwaardelijke toegang van Azure om gebruikers de mogelijkheid te bieden om te communiceren met Azure Resource Manager door ' blok toegang ' te configureren voor de app Microsoft Azure management.

- [Voorwaardelijke toegang configureren om de toegang tot Azure Resource Manager te blok keren](../role-based-access-control/conditional-access-azure-management.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

## <a name="secure-configuration"></a>Veilige configuratie

*Zie [Azure Security Bench Mark: Secure Configuration](../security/benchmarks/security-control-secure-configuration.md)(Engelstalig) voor meer informatie.*

### <a name="71-establish-secure-configurations-for-all-azure-resources"></a>7,1: veilige configuraties instellen voor alle Azure-resources

**Hulp**: Definieer en implementeer standaard beveiligings configuraties voor uw Azure service bus-implementaties. U kunt ook gebruik maken van ingebouwde beleids definities voor Azure Service Bus, zoals:

- Diagnostische logboeken in Service Bus moeten zijn ingeschakeld
- Service Bus moet een service-eind punt van een virtueel netwerk gebruiken om het netwerk verkeer naar uw particuliere netwerken te beperken.

Gebruik Azure Policy aliassen in de naam ruimte ' micro soft. ServiceBus ' om aangepaste beleids regels te maken om configuraties te controleren of af te dwingen.

- [Ingebouwde beleids regels voor Azure voor Service Bus ](./policy-reference.md)

- [Beschik bare Azure Policy aliassen weer geven](/powershell/module/az.resources/get-azpolicyalias?view=azps-3.3.0)

- [Azure Policy configureren en beheren](../governance/policy/tutorials/create-and-manage.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="73-maintain-secure-azure-resource-configurations"></a>7,3: Beveilig Azure-resource configuraties onderhouden

**Hulp**: gebruik Azure Policy [deny] en [implementeren indien niet aanwezig] voor het afdwingen van beveiligde instellingen voor uw service bus-compatibele resources of toepassingen.

- [Azure Policy configureren en beheren](../governance/policy/tutorials/create-and-manage.md)

- [Voor meer informatie over de Azure Policy effecten](../governance/policy/concepts/effects.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="77-deploy-configuration-management-tools-for-azure-resources"></a>7,7: hulpprogram ma's voor configuratie beheer voor Azure-resources implementeren

**Hulp**: gebruik Azure Policy aliassen in de naam ruimte ' micro soft. ServiceBus ' om aangepaste beleids regels te maken om systeem configuraties te Signa lering, te controleren en af te dwingen. Ontwikkel bovendien een proces en pijp lijn voor het beheren van beleids uitzonderingen.

- [Azure Policy configureren en beheren](../governance/policy/tutorials/create-and-manage.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="79-implement-automated-configuration-monitoring-for-azure-resources"></a>7,9: geautomatiseerde configuratie bewaking voor Azure-resources implementeren

**Hulp**: gebruik Azure Policy aliassen in de naam ruimte ' micro soft. ServiceBus ' om aangepaste beleids regels te maken om systeem configuraties te Signa lering, te controleren en af te dwingen. Gebruik Azure Policy [audit], [deny] en [implementeren indien niet aanwezig] om automatisch configuraties af te dwingen voor uw Azure Service Bus implementaties en gerelateerde bronnen.

- [Azure Policy configureren en beheren](../governance/policy/tutorials/create-and-manage.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="711-manage-azure-secrets-securely"></a>7,11: Azure-geheimen veilig beheren

**Richt lijnen**: voor virtuele machines van Azure of webtoepassingen die worden uitgevoerd op Azure app service worden gebruikt voor toegang tot uw service bus entiteiten, gebruikt u een Managed Service Identity in combi natie met Azure Key Vault om het beheer van gedeelde toegang voor uw Azure service bus-implementaties te vereenvoudigen en te beveiligen. Zorg ervoor Key Vault zacht verwijderen is ingeschakeld.

- [Een beheerde identiteit verifiëren met Azure Active Directory om toegang te krijgen tot Service Bus bronnen](service-bus-managed-service-identity.md)

- [Door de klant beheerde sleutels voor Service Bus configureren](configure-customer-managed-key.md)

- [Een Key Vault maken](../key-vault/general/quick-create-portal.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="712-manage-identities-securely-and-automatically"></a>7,12: identiteiten veilig en automatisch beheren

**Richt lijnen**: voor virtuele machines van Azure of webtoepassingen die worden uitgevoerd op Azure app service worden gebruikt voor toegang tot uw service bus entiteiten, gebruikt u Managed Service Identity in combi natie met Azure Key Vault om Azure service bus te vereenvoudigen en te beveiligen. Zorg ervoor Key Vault zacht verwijderen is ingeschakeld.

Gebruik beheerde identiteiten om Azure-Services te voorzien van een automatisch beheerde identiteit in Azure Active Directory (Azure AD). Met beheerde identiteiten kunt u zich verifiëren bij elke service die ondersteuning biedt voor Azure AD-verificatie, met inbegrip van Azure Key Vault, zonder enige referenties in uw code.

- [Een beheerde identiteit verifiëren met Azure Active Directory om toegang te krijgen tot Service Bus bronnen](service-bus-managed-service-identity.md)

- [Door de klant beheerde sleutels voor Service Bus configureren](configure-customer-managed-key.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="713-eliminate-unintended-credential-exposure"></a>7,13: onbedoelde referentie blootstelling elimineren

**Richt lijnen**: referentie scanner implementeren om referenties in code te identificeren. Referentie scanner stimuleert ook het verplaatsen van gedetecteerde referenties naar veiliger locaties, zoals Azure Key Vault.

- [Referentie scanner instellen](https://secdevtools.azurewebsites.net/helpcredscan.html)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

## <a name="malware-defense"></a>Beveiliging tegen malware

*Zie voor meer informatie de [Azure Security Bench Mark: beveiliging tegen schadelijke software](../security/benchmarks/security-control-malware-defense.md).*

### <a name="82-pre-scan-files-to-be-uploaded-to-non-compute-azure-resources"></a>8,2: scan bestanden die moeten worden geüpload naar niet-reken resources van Azure

**Richt lijnen**: het vooraf scannen van inhoud die wordt geüpload naar niet-reken resources van Azure, zoals Azure Service Bus, App Service, Data Lake Storage, Blob Storage, Azure database for PostgreSQL, enzovoort. Micro soft heeft geen toegang tot uw gegevens in deze instanties.

Micro soft anti-malware is ingeschakeld op de onderliggende host die ondersteuning biedt voor Azure-Services, maar wordt niet uitgevoerd op de inhoud van de klant.

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: gedeeld

## <a name="data-recovery"></a>Gegevensherstel

*Zie [Azure Security Bench Mark: Data Recovery](../security/benchmarks/security-control-data-recovery.md)(Engelstalig) voor meer informatie.*

### <a name="91-ensure-regular-automated-back-ups"></a>9,1: zorg voor regel matige automatische back-ups

**Hulp** bij het configureren van geo-nood herstel voor Azure service bus. Als er voor de hele Azure-regio's of-Data Centers (als er geen beschikbaarheids zones worden gebruikt) downtime actief is, is het van essentieel belang dat de gegevens worden verwerkt in een andere regio of Data Center. Daarom zijn geo-nood herstel en geo-replicatie belang rijke functies voor elke onderneming. Azure Service Bus ondersteunt zowel geo-nood herstel als geo-replicatie op het niveau van de naam ruimte.

- [Meer informatie over geografisch nood herstel voor Azure Service Bus](service-bus-geo-dr.md)

**Azure Security Center bewaking**: momenteel niet beschikbaar

**Verantwoordelijkheid**: klant

### <a name="92-perform-complete-system-backups-and-backup-any-customer-managed-keys"></a>9,2: volledige back-ups van het systeem uitvoeren en een back-up maken van door de klant beheerde sleutels

**Hulp**: Azure service bus zorgt voor versleuteling van gegevens in rust met Azure Storage-service versleuteling (Azure SSE). Service Bus is afhankelijk van Azure Storage om de gegevens op te slaan en standaard worden alle gegevens die zijn opgeslagen met Azure Storage versleuteld met door micro soft beheerde sleutels. Als u Azure Key Vault gebruikt voor het opslaan van door de klant beheerde sleutels, zorgt u voor regel matige automatische back-ups van uw sleutels.

Zorg voor regel matige automatische back-ups van uw Key Vault geheimen met de volgende Power shell-opdracht: Backup-AzKeyVaultSecret

- [Door de klant beheerde sleutels configureren voor het versleutelen van Azure Service Bus gegevens in rust](configure-customer-managed-key.md)

- [Back-ups maken van Key Vault geheimen](/powershell/module/azurerm.keyvault/backup-azurekeyvaultsecret)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="93-validate-all-backups-including-customer-managed-keys"></a>9,3: alle back-ups valideren, inclusief door de klant beheerde sleutels

**Richt lijnen**: herstel van back-ups van door de klant beheerde sleutels gebruiken om Service Bus gegevens te versleutelen.

- [Door de klant beheerde sleutels configureren voor het versleutelen van Azure Service Bus gegevens in rust](configure-customer-managed-key.md)

- [Sleutel kluis sleutels herstellen in azure](/powershell/module/azurerm.keyvault/restore-azurekeyvaultkey?view=azurermps-6.13.0)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="94-ensure-protection-of-backups-and-customer-managed-keys"></a>9,4: zorg voor de bescherming van back-ups en door de klant beheerde sleutels

**Hulp**: Schakel zacht verwijderen in Key Vault in om sleutels te beschermen tegen onbedoelde of schadelijke verwijdering. Azure Service Bus moet door de klant beheerde sleutels worden verwijderd en niet zijn geconfigureerd.

- [Zacht verwijderen inschakelen in Key Vault](../storage/blobs/soft-delete-blob-overview.md?tabs=azure-portal)

- [Een sleutel kluis met sleutels instellen](../event-hubs/configure-customer-managed-key.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

## <a name="incident-response"></a>Reageren op incidenten

*Zie [Azure Security Bench Mark: Incident Response](../security/benchmarks/security-control-incident-response.md)(Engelstalig) voor meer informatie.*

### <a name="101-create-an-incident-response-guide"></a>10,1: een hand leiding voor reactie op incidenten maken

**Hulp**: een antwoord gids voor incidenten ontwikkelen voor uw organisatie. Zorg ervoor dat er schriftelijke incidenten abonnementen zijn die alle personeels rollen definiëren, evenals de fasen van het verwerken van incidenten en het beheer van de detectie tot een beoordeling van het incident. 

- [Richt lijnen voor het bouwen van uw eigen beveiligings incident antwoord proces](https://msrc-blog.microsoft.com/2019/07/01/inside-the-msrc-building-your-own-security-incident-response-process/) 

- [Micro soft Security Response Center anatomie van een incident](https://msrc-blog.microsoft.com/2019/06/27/inside-the-msrc-anatomy-of-a-ssirp-incident/) 

- [De verwerkings gids voor het computer beveiligings incident van het NIST gebruiken om u te helpen bij het maken van uw eigen reactie plan voor incidenten](https://csrc.nist.gov/publications/detail/sp/800-61/rev-2/final)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="102-create-an-incident-scoring-and-prioritization-procedure"></a>10,2: een beoordelings procedure voor incidenten en prioriteits procedures maken

**Hulp**: Azure Security Center wijst aan elke waarschuwing een Ernst toe om u te helpen bepalen welke waarschuwingen het eerst moeten worden onderzocht. De ernst is gebaseerd op de manier waarop vertrouwen Security Center is in de zoek actie of het analyse programma dat wordt gebruikt om de waarschuwing te geven, evenals het betrouwbaarheids niveau dat er schadelijke bedoelingen zijn achter de activiteit die tot de waarschuwing heeft geleid.

Markeer bovendien abonnementen met tags en maak een naamgevings systeem voor het identificeren en categoriseren van Azure-resources, met name voor de verwerking van gevoelige gegevens. Het is uw verantwoordelijkheid om prioriteit te geven aan het herstel van waarschuwingen op basis van de ernst van de Azure-resources en-omgeving waar het incident heeft plaatsgevonden. 

- [Beveiligingswaarschuwingen in Azure Security Center](../security-center/security-center-alerts-overview.md) 

- [Tags gebruiken om Azure-resources te organiseren](../azure-resource-manager/management/tag-resources.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="103-test-security-response-procedures"></a>10,3: procedures voor beveiligings antwoorden testen

**Richt lijnen**: oefent oefeningen uit om de respons mogelijkheden van uw systeem op een gewone uitgebracht te testen. Identificeer zwakke punten en tussen ruimten en wijzig zo nodig het schema.

- [Publicatie van het NIST: hand leiding voor het testen, trainen en uitoefenen van Program Ma's voor IT-plannen en-mogelijkheden](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-84.pdf)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="104-provide-security-incident-contact-details-and-configure-alert-notifications-for-security-incidents"></a>10,4: contact gegevens van het beveiligings incident opgeven en waarschuwings meldingen configureren voor beveiligings incidenten

**Hulp**: contact gegevens van beveiligings incidenten worden door micro soft gebruikt om contact met u op te nemen als het micro soft Security Response Center (MSRC) detecteert dat uw gegevens zijn geopend door een onrecht matige of niet-gemachtigde partij. Bekijk incidenten na het feit om te controleren of de problemen zijn opgelost. 

- [De Azure Security Center Security-contact persoon instellen](../security-center/security-center-provide-security-contact-details.md)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="105-incorporate-security-alerts-into-your-incident-response-system"></a>10,5: beveiligings waarschuwingen opnemen in uw reactie systeem van uw incident

**Hulp**: exporteer uw Azure Security Center waarschuwingen en aanbevelingen met behulp van de functie continue export om Risico's voor Azure-resources te identificeren. Met doorlopend exporteren kunt u waarschuwingen en aanbevelingen hand matig of op een doorlopende manier exporteren. U kunt de Azure Security Center Data Connector gebruiken om de waarschuwingen naar Azure Sentinel te streamen. 

- [Continue export configureren](../security-center/continuous-export.md) 

- [Waarschuwingen streamen naar Azure Sentinel](../sentinel/connect-azure-security-center.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="106-automate-the-response-to-security-alerts"></a>10,6: de reactie op beveiligings waarschuwingen automatiseren

**Hulp**: 

Gebruik de functie werk stroom automatisering Azure Security Center om automatisch reacties te activeren op beveiligings waarschuwingen en aanbevelingen voor het beveiligen van uw Azure-resources. 

- [Werk stroom automatisering configureren in Security Center](../security-center/workflow-automation.md)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

## <a name="penetration-tests-and-red-team-exercises"></a>Penetratietests en Red Team-oefeningen

*Zie [Azure Security Bench Mark: Indringings tests en rode team oefeningen](../security/benchmarks/security-control-penetration-tests-red-team-exercises.md)voor meer informatie.*

### <a name="111-conduct-regular-penetration-testing-of-your-azure-resources-and-ensure-remediation-of-all-critical-security-findings"></a>11,1: voert regel matig indringings tests van uw Azure-resources uit en zorgt voor herbemiddeling van alle essentiële beveiligings resultaten

**Richt lijnen**: Volg de stappen voor het testen van de Microsoft Cloud indringings regels om ervoor te zorgen dat uw indringings tests niet worden geschonden door het micro soft-beleid. Gebruik de strategie van micro soft en de uitvoering van de implementatie van de indringing van een live site in de Cloud, services en toepassingen die door micro soft worden beheerd. 

- [Regels van betrokkenheid voor het testen van indringing](https://www.microsoft.com/msrc/pentest-rules-of-engagement?rtc=1) 

- [Microsoft Cloud rode teams](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: gedeeld

## <a name="next-steps"></a>Volgende stappen

- Zie de [Azure Security-Bench Mark](../security/benchmarks/overview.md)
- Meer informatie over [Azure-beveiligings basislijnen](../security/benchmarks/security-baselines-overview.md)