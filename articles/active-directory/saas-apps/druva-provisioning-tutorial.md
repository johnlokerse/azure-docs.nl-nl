---
title: 'Zelfstudie: Druva configureren voor automatische inrichting van gebruikers met Azure Active Directory | Microsoft Docs'
description: Ontdek hoe u Azure Active Directory configureert om gebruikersaccounts automatisch in te richten en de inrichting van gebruikersaccounts ongedaan te maken voor Druva.
services: active-directory
author: zchia
writer: zchia
manager: CelesteDG
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 07/26/2019
ms.author: zhchia
ms.openlocfilehash: 5579a9d96828caa1453547e7c2e11b8f0d717d2a
ms.sourcegitcommit: 0b9fe9e23dfebf60faa9b451498951b970758103
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/07/2020
ms.locfileid: "94359303"
---
# <a name="tutorial-configure-druva-for-automatic-user-provisioning"></a>Zelfstudie: Druva configureren voor automatische gebruikersinrichting

Het doel van deze zelfstudie is om de stappen te laten zien die moeten worden uitgevoerd in Druva en Azure Active Directory (Azure AD) om Azure AD te configureren voor het automatisch inrichten en het ongedaan maken van de inrichting van gebruikers en/of groepen voor Druva.

> [!NOTE]
> In deze zelfstudie wordt een connector beschreven die is gebaseerd op de Azure AD-service voor het inrichten van gebruikers. Zie voor belangrijke details over wat deze service doet, hoe het werkt en veelgestelde vragen [Inrichting en ongedaan maken van inrichting van gebruikers automatiseren naar SaaS-toepassingen met Azure Active Directory](../app-provisioning/user-provisioning.md).
>
> Deze connector is momenteel beschikbaar in openbare preview. Zie voor meer informatie over de algemene Microsoft Azure-gebruiksvoorwaarden voor preview-functies [Aanvullende gebruiksvoorwaarden voor Microsoft Azure-previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## <a name="prerequisites"></a>Vereisten

In het scenario dat in deze zelfstudie wordt beschreven, wordt ervan uitgegaan dat u al beschikt over de volgende vereisten:

* Een Azure AD-tenant.
* [Een Druva-tenant](https://www.druva.com/products/pricing-plans/).
* Een gebruikersaccount in Druva met beheerdersmachtigingen.

## <a name="assigning-users-to-druva"></a>Gebruikers toewijzen aan Druva

Azure Active Directory gebruikt een concept dat *toewijzingen* wordt genoemd om te bepalen welke gebruikers toegang moeten krijgen tot geselecteerde apps. In de context van het automatisch inrichten van gebruikers worden alleen de gebruikers en/of groepen gesynchroniseerd die zijn toegewezen aan een toepassing in Azure AD.

Voordat u automatische inrichting van gebruikers configureert en inschakelt, moet u beslissen welke gebruikers en/of groepen in Azure AD toegang nodig hebben tot Druva. Als u dit eenmaal hebt besloten, kunt u deze gebruikers en/of groepen aan Druva toewijzen door de instructies hier te volgen:
* [Een gebruiker of groep toewijzen aan een bedrijfs-app](../manage-apps/assign-user-or-group-access-portal.md)

## <a name="important-tips-for-assigning-users-to-druva"></a>Belangrijke tips voor het toewijzen van gebruikers aan Druva

* Het wordt aanbevolen om eerst één Azure AD-gebruiker toe te wijzen aan Druva om de configuratie van de automatische gebruikersinrichting te testen. Extra gebruikers en/of groepen kunnen dan later worden toegewezen.

* Als u een gebruiker aan Druva toewijst, moet u een geldige toepassingsspecifieke rol (indien beschikbaar) selecteren in het toewijzingsdialoogvenster. Gebruikers met de rol **Standaard toegang** worden uitgesloten van het inrichten.

## <a name="setup-druva-for-provisioning"></a>Druva instellen voor inrichting

Voordat u Druva configureert voor het automatisch inrichten van gebruikers met Azure AD, moet u SCIM-inrichting inschakelen in Druva.

1. Meld u aan bij de [beheerconsole van Druva](https://console.druva.com). Ga naar **Druva > inSync**.

    ![Beheerconsole van Druva](media/druva-provisioning-tutorial/menubar.png)

2. Ga naar **Manage** > **Deployments** > **Users**.

    :::image type="content" source="media/druva-provisioning-tutorial/manage.png" alt-text="Schermopname van de beheerconsole van Druva. Beheren is gemarkeerd en de opties in het menu zijn zichtbaar. In dat menu is onder Deployments de optie Users gemarkeerd." border="false":::

3.  Ga naar **Settings**. Klik op **Generate Token**.

    :::image type="content" source="media/druva-provisioning-tutorial/settings.png" alt-text="Schermopname van een pagina in de beheerconsole van Druva. Settings is gemarkeerd en het tabblad Settings is open. De knop Generate Token is gemarkeerd." border="false":::

4.  Kopieer de waarde van **Auth token**. Deze waarde wordt ingevoerd in het veld **Token voor geheim** op het tabblad Inrichten van de Druva-toepassing in Azure Portal.
    
    :::image type="content" source="media/druva-provisioning-tutorial/auth.png" alt-text="Schermopname van de pagina Create Token in de beheerconsole van Druva. Er is een link met het label Copy Token beschikbaar voor het kopiëren van de waarde van het autorisatietoken." border="false":::

## <a name="add-druva-from-the-gallery"></a>Druva toevoegen vanuit de galerie

Als u Druva wilt configureren voor het automatisch inrichten van gebruikers met Azure AD, moet u Druva vanuit de Azure AD-toepassingsgalerie toevoegen aan uw lijst met beheerde SaaS-toepassingen.

**Voer de volgende stappen uit om Druva toe te voegen vanuit de Azure AD-toepassingsgalerie:**

1. Ga naar **[Azure Portal](https://portal.azure.com)** en selecteer **Azure Active Directory** in het navigatievenster aan de linkerkant.

    ![De knop Azure Active Directory](common/select-azuread.png)

2. Ga naar **Bedrijfstoepassingen** en selecteer vervolgens **Alle toepassingen**.

    ![De blade Bedrijfstoepassingen](common/enterprise-applications.png)

3. Als u een nieuwe toepassing wilt toevoegen, selecteert u de knop **Nieuwe toepassing** bovenin het deelvenster.

    ![De knop Nieuwe toepassing](common/add-new-app.png)

4. Typ **Druva** in het zoekvak, selecteer **Druva** in het venster met resultaten en klik op de knop **Toevoegen** om de toepassing toe te voegen.

    ![Druva in de lijst met resultaten](common/search-new-app.png)

## <a name="configuring-automatic-user-provisioning-to-druva"></a>Automatische gebruikersinrichting voor Druva configureren 

In deze sectie wordt u begeleid bij de stappen voor het configureren van de Azure AD-inrichtingsservice om gebruikers en/of groepen in Druva te maken, bij te werken en uit te schakelen op basis van gebruikers- en/of groepstoewijzingen in Azure AD.

> [!TIP]
> U kunt er ook voor kiezen om eenmalige aanmelding op basis van SAML in te schakelen voor Druva, waarvoor u de instructies in de [Zelfstudie eenmalige aanmelding voor Druva](druva-tutorial.md) moet volgen. Eenmalige aanmelding kan onafhankelijk van automatische inrichting van gebruikers worden geconfigureerd, maar deze twee functies vullen elkaar aan.

### <a name="to-configure-automatic-user-provisioning-for-druva-in-azure-ad"></a>Automatische gebruikersinrichting configureren voor Druva in Azure AD:

1. Meld u aan bij de [Azure-portal](https://portal.azure.com). Selecteer **Bedrijfstoepassingen** en vervolgens **Alle toepassingen**.

    ![De blade Bedrijfstoepassingen](common/enterprise-applications.png)

2. Selecteer in de lijst met toepassingen **Druva**.

    ![De Druva-link in de lijst met toepassingen](common/all-applications.png)

3. Selecteer het tabblad **Inrichten**.

    ![Schermopname van de beheeropties met de optie 'Inrichting' gemarkeerd.](common/provisioning.png)

4. Stel de **Inrichtingsmodus** in op **Automatisch**.

    ![Schermopname van de vervolgkeuzelijst Inrichtingsmodus met de optie Automatisch gemarkeerd.](common/provisioning-automatic.png)

5.  Voer in de sectie Referenties voor beheerder `https://apis.druva.com/insync/scim` in bij **Tenant-URL**. Voer de waarde van **Auth token** in bij **Token voor geheim**. Klik op **Verbinding testen** om te controleren of Azure AD verbinding kan maken met Druva. Als de verbinding mislukt, moet u controleren of uw Druva-account beheerdersmachtigingen heeft. Probeer het daarna opnieuw.

    ![Tenant-URL + token](common/provisioning-testconnection-tenanturltoken.png)

6. Voer in het veld **E-mailadres voor meldingen** het e-mailadres in van een persoon of groep die de inrichtingsfoutmeldingen zou moeten ontvangen en schakel het selectievakje **Een e-mailmelding verzenden als een fout optreedt** in.

    ![E-mailadres voor meldingen](common/provisioning-notification-email.png)

7. Klik op **Opslaan**.

8. Selecteer in de sectie **Toewijzingen** de optie **Azure Active Directory-gebruikers synchroniseren met Druva**.

    ![Toewijzingen van Druva-gebruikers](media/druva-provisioning-tutorial/usermapping.png)

9. Controleer in de sectie **Kenmerktoewijzingen** de gebruikerskenmerken die vanuit Azure AD met Druva worden gesynchroniseerd. De kenmerken die als **overeenkomende** eigenschappen zijn geselecteerd, worden gebruikt om de gebruikersaccounts in Druva te vinden voor updatebewerkingen. Selecteer de knop **Opslaan** om eventuele wijzigingen door te voeren.

    ![Druva-gebruikerskenmerken ophalen](media/druva-provisioning-tutorial/userattribute.png)


10. Als u bereikfilters wilt configureren, raadpleegt u de volgende instructies in de [zelfstudie Bereikfilter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md).

11. Wijzig **Inrichtingsstatus** in **Aan** in de sectie **Instellingen** om de Azure AD-inrichtingsservice in te schakelen voor Druva.

    ![Inrichtingsstatus ingeschakeld](common/provisioning-toggle-on.png)

12. Definieer de gebruikers en/of groepen die u aan Druva wilt toevoegen door de gewenste waarden te kiezen bij **Bereik** in de sectie **Instellingen**.

    ![Inrichtingsbereik](common/provisioning-scope.png)

13. Wanneer u klaar bent om in te richten, klikt u op **Opslaan**.

    ![Inrichtingsconfiguratie opslaan](common/provisioning-configuration-save.png)

    Met deze bewerking wordt de eerste synchronisatie gestart van alle gebruikers en/of groepen die zijn gedefinieerd onder **Bereik** in de sectie **Instellingen**. De initiële synchronisatie duurt langer dan volgende synchronisaties, die ongeveer om de 40 minuten plaatsvinden zolang de Azure AD-inrichtingsservice wordt uitgevoerd. U kunt het gedeelte **Synchronisatiedetails** gebruiken om de voortgang te controleren en koppelingen te volgen naar het activiteitenrapport van de inrichting, waarin alle acties worden beschreven die door de Azure AD-inrichtingsservice in Druva worden uitgevoerd.

    Zie [Rapportage over automatische inrichting van gebruikersaccounts](../app-provisioning/check-status-user-account-provisioning.md) voor informatie over het lezen van de Azure AD-inrichtingslogboeken.
    
## <a name="connector-limitations"></a>Connectorbeperkingen

* Voor Druva is **email** als verplicht kenmerk vereist. 

## <a name="additional-resources"></a>Aanvullende resources

* [De inrichting van gebruikersaccounts voor bedrijfstoepassingen beheren](../app-provisioning/configure-automatic-user-provisioning-portal.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md) (Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?)

## <a name="next-steps"></a>Volgende stappen

* [Informatie over het controleren van logboeken en het ophalen van rapporten over inrichtingsactiviteit](../app-provisioning/check-status-user-account-provisioning.md)
