---
title: Een aangepaste NGINX ingangs controller gebruiken en HTTPS configureren
services: azure-dev-spaces
ms.date: 12/10/2019
ms.topic: conceptual
description: Meer informatie over het configureren van Azure dev Spaces voor het gebruik van een aangepaste NGINX ingress-controller en het configureren van HTTPS met deze ingangs controller
keywords: Docker, Kubernetes, Azure, AKS, Azure Kubernetes Service, containers, Helm, servicemesh, servicemeshroutering, kubectl, k8s
ms.custom: devx-track-js, devx-track-azurecli
ms.openlocfilehash: e1918b5ce9c0fdba81174f0b36fd1ce51d0df70a
ms.sourcegitcommit: 8c7f47cc301ca07e7901d95b5fb81f08e6577550
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/27/2020
ms.locfileid: "92748822"
---
# <a name="use-a-custom-nginx-ingress-controller-and-configure-https"></a>Een aangepaste NGINX ingangs controller gebruiken en HTTPS configureren

[!INCLUDE [Azure Dev Spaces deprecation](../../../includes/dev-spaces-deprecation.md)]

In dit artikel leest u hoe u Azure dev Spaces configureert voor het gebruik van een aangepaste NGINX ingress-controller. In dit artikel leest u ook hoe u die aangepaste ingangs controller configureert voor het gebruik van HTTPS.

## <a name="prerequisites"></a>Vereisten

* Een Azure-abonnement. Als u nog geen account hebt, kunt u [een gratis account aanmaken][azure-account-create].
* [Azure CLI geïnstalleerd][az-cli].
* Azure Kubernetes service (AKS)-cluster waarvoor Azure dev Spaces zijn ingeschakeld.
* [kubectl][kubectl] is geïnstalleerd.
* [Helm 3 is geïnstalleerd][helm-installed].
* [Een aangepast domein][custom-domain] met een [DNS-zone][dns-zone].  In dit artikel wordt ervan uitgegaan dat de aangepaste domein-en DNS-zone zich in dezelfde resource groep bevinden als uw AKS-cluster, maar het is wel mogelijk om een aangepast domein en een DNS-zone in een andere resource groep te gebruiken.

## <a name="configure-a-custom-nginx-ingress-controller"></a>Een aangepaste NGINX ingress-controller configureren

Maak verbinding met uw cluster met behulp van [kubectl][kubectl], de Kubernetes-opdracht regel-client. Gebruik de opdracht [az aks get-credentials][az-aks-get-credentials] om `kubectl` zodanig te configureren dat er verbinding wordt gemaakt met het Kubernetes-cluster. Bij deze opdracht worden referenties gedownload en wordt Kubernetes CLI geconfigureerd voor het gebruik van deze referenties.

```azurecli
az aks get-credentials --resource-group myResourceGroup --name myAKS
```

Als u de verbinding met uw cluster wilt controleren, gebruikt u de opdracht [kubectl get][kubectl-get] om een lijst met clusterknooppunten te retourneren.

```console
kubectl get nodes
NAME                                STATUS   ROLES   AGE    VERSION
aks-nodepool1-12345678-vmssfedcba   Ready    agent   13m    v1.14.1
```

Voeg de [officiële stabiele helm-opslag plaats][helm-stable-repo]toe, die de helm-grafiek van de NGINX ingress-controller bevat.

```console
helm repo add stable https://kubernetes-charts.storage.googleapis.com/
```

Maak een Kubernetes-naam ruimte voor de NGINX ingangs controller en installeer deze met behulp van `helm` .

```console
kubectl create ns nginx
helm install nginx stable/nginx-ingress --namespace nginx --version 1.27.0
```

> [!NOTE]
> In het bovenstaande voor beeld wordt een openbaar eind punt gemaakt voor uw ingangs controller. Als u in plaats daarvan een persoonlijk eind punt voor uw ingangs controller moet gebruiken, voegt u de *--set controller. service. annotaties toe. service \\ . beta \\ . kubernetes \\ . io/Azure-Load-Balancer-internal "= True* para meter voor de *installatie opdracht helm* . Bijvoorbeeld:
> ```console
> helm install nginx stable/nginx-ingress --namespace nginx --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-internal"=true --version 1.27.0
> ```
> Dit persoonlijke eind punt wordt weer gegeven in het virtuele netwerk waar u AKS-cluster wordt geïmplementeerd.

Haal het IP-adres van de NGINX ingress-controller service op met behulp van [kubectl Get][kubectl-get].

```console
kubectl get svc -n nginx --watch
```

In de voorbeeld uitvoer ziet u de IP-adressen voor alle services in de *nginx* -naam ruimte.

```console
NAME                                  TYPE           CLUSTER-IP     EXTERNAL-IP      PORT(S)                      AGE
nginx-nginx-ingress-controller        LoadBalancer   10.0.19.39     <pending>        80:31314/TCP,443:30521/TCP   10s
nginx-nginx-ingress-default-backend   ClusterIP      10.0.210.231   <none>           80/TCP                       10s
...
nginx-nginx-ingress-controller        LoadBalancer   10.0.19.39     MY_EXTERNAL_IP   80:31314/TCP,443:30521/TCP   26s
```

Voeg een *A* -record toe aan uw DNS-zone met het externe IP-adres van de NGINX-service met [AZ Network DNS record-set A add-record][az-network-dns-record-set-a-add-record].

```azurecli
az network dns record-set a add-record \
    --resource-group myResourceGroup \
    --zone-name MY_CUSTOM_DOMAIN \
    --record-set-name *.nginx \
    --ipv4-address MY_EXTERNAL_IP
```

In het bovenstaande voor beeld wordt een *A* -record toegevoegd aan de DNS-zone *MY_CUSTOM_DOMAIN* .

In dit artikel gebruikt u de [voorbeeld toepassing delen van Azure dev Spaces Bike](https://github.com/Azure/dev-spaces/tree/master/samples/BikeSharingApp) om te demonstreren hoe u Azure dev Spaces gebruikt. Kloon de toepassing uit GitHub en navigeer naar de bijbehorende map:

```cmd
git clone https://github.com/Azure/dev-spaces
cd dev-spaces/samples/BikeSharingApp/charts
```

Open [Values. yaml][values-yaml] en voer de volgende updates uit:
* Alle exemplaren van *<REPLACE_ME_WITH_HOST_SUFFIX>* vervangen door *nginx. MY_CUSTOM_DOMAIN* uw domein gebruiken voor *MY_CUSTOM_DOMAIN* . 
* Vervang *kubernetes.io/ingress.class: traefik-azds # dev Spaces-specifiek* met *kubernetes.io/ingress.class: nginx # aangepaste* inkomend verkeer. 

Hieronder ziet u een voor beeld van een bijgewerkt `values.yaml` bestand:

```yaml
# This is a YAML-formatted file.
# Declare variables to be passed into your templates.

bikesharingweb:
  ingress:
    annotations:
      kubernetes.io/ingress.class: nginx  # Custom Ingress
    hosts:
      - dev.bikesharingweb.nginx.MY_CUSTOM_DOMAIN  # Assumes deployment to the 'dev' space

gateway:
  ingress:
    annotations:
      kubernetes.io/ingress.class: nginx  # Custom Ingress
    hosts:
      - dev.gateway.nginx.MY_CUSTOM_DOMAIN  # Assumes deployment to the 'dev' space
```

Sla de wijzigingen op en sluit het bestand.

Maak de *ontwikkelings* ruimte met uw voorbeeld toepassing met behulp van `azds space select` .

```console
azds space select -n dev -y
```

Implementeer de voorbeeld toepassing met behulp van `helm install` .

```console
helm install bikesharingsampleapp . --dependency-update --namespace dev --atomic
```

In het bovenstaande voor beeld wordt de voorbeeld toepassing geïmplementeerd in de naam ruimte voor *ontwikkel aars* .

De Url's weer geven voor toegang tot de voorbeeld toepassing met behulp van `azds list-uris` .

```console
azds list-uris
```

In de onderstaande uitvoer ziet u de voor beeld-Url's van `azds list-uris` .

```console
Uri                                                  Status
---------------------------------------------------  ---------
http://dev.bikesharingweb.nginx.MY_CUSTOM_DOMAIN/  Available
http://dev.gateway.nginx.MY_CUSTOM_DOMAIN/         Available
```

Ga naar de *bikesharingweb* -service door de open bare URL te openen via de `azds list-uris` opdracht. In het bovenstaande voor beeld is de open bare URL voor de *bikesharingweb* -service `http://dev.bikesharingweb.nginx.MY_CUSTOM_DOMAIN/` .

> [!NOTE]
> Als er een fout pagina wordt weer geven in plaats van de *bikesharingweb* -service, controleert u of u **zowel** de *kubernetes.io/ingress.class* aantekening als de host in het bestand *Values. yaml* hebt bijgewerkt.

Gebruik de `azds space select` opdracht om een onderliggende ruimte onder *dev* te maken en geef de url's weer om toegang te krijgen tot de onderliggende dev-ruimte.

```console
azds space select -n dev/azureuser1 -y
azds list-uris
```

De onderstaande uitvoer toont de voor beeld-Url's van `azds list-uris` om toegang te krijgen tot de voorbeeld toepassing in de *azureuser1* onderliggende ontwikkel ruimte.

```console
Uri                                                  Status
---------------------------------------------------  ---------
http://azureuser1.s.dev.bikesharingweb.nginx.MY_CUSTOM_DOMAIN/  Available
http://azureuser1.s.dev.gateway.nginx.MY_CUSTOM_DOMAIN/         Available
```

Ga naar de *bikesharingweb* -service in de *azureuser1* -onderliggende ontwikkel ruimte door de open bare URL te openen via de `azds list-uris` opdracht. In het bovenstaande voor beeld is de open bare URL voor de *bikesharingweb* -service in de *azureuser1* -ruimte voor de onderliggende ontwikkel aars `http://azureuser1.s.dev.bikesharingweb.nginx.MY_CUSTOM_DOMAIN/` .

## <a name="configure-the-nginx-ingress-controller-to-use-https"></a>De NGINX ingress-controller configureren voor het gebruik van HTTPS

Gebruik [CERT-Manager][cert-manager] om het beheer van het TLS-certificaat te automatiseren bij het configureren van uw NGINX ingress-controller voor het gebruik van HTTPS. Gebruiken `helm` om de *certmanager* -grafiek te installeren.

```console
kubectl apply --validate=false -f https://raw.githubusercontent.com/jetstack/cert-manager/release-0.12/deploy/manifests/00-crds.yaml --namespace nginx
kubectl label namespace nginx certmanager.k8s.io/disable-validation=true
helm repo add jetstack https://charts.jetstack.io
helm repo update
helm install cert-manager --namespace nginx --version v0.12.0 jetstack/cert-manager --set ingressShim.defaultIssuerName=letsencrypt --set ingressShim.defaultIssuerKind=ClusterIssuer
```

Maak een `letsencrypt-clusterissuer.yaml` bestand en werk het e-mail veld bij met uw e-mail adres.

```yaml
apiVersion: cert-manager.io/v1alpha2
kind: ClusterIssuer
metadata:
  name: letsencrypt
spec:
  acme:
    server: https://acme-v02.api.letsencrypt.org/directory
    email: MY_EMAIL_ADDRESS
    privateKeySecretRef:
      name: letsencrypt
    solvers:
      - http01:
          ingress:
            class: nginx
```

> [!NOTE]
> Voor het testen kunt u ook een [staging-server][letsencrypt-staging-issuer] gebruiken voor uw *ClusterIssuer* .

Gebruiken `kubectl` om toe te passen `letsencrypt-clusterissuer.yaml` .

```console
kubectl apply -f letsencrypt-clusterissuer.yaml --namespace nginx
```

Update [Values. yaml][values-yaml] om de Details voor het gebruik van *CERT-beheer* en HTTPS op te neemt. Hieronder ziet u een voor beeld van een bijgewerkt `values.yaml` bestand:

```yaml
# This is a YAML-formatted file.
# Declare variables to be passed into your templates.

bikesharingweb:
  ingress:
    annotations:
      kubernetes.io/ingress.class: nginx  # Custom Ingress
      cert-manager.io/cluster-issuer: letsencrypt
    hosts:
      - dev.bikesharingweb.nginx.MY_CUSTOM_DOMAIN  # Assumes deployment to the 'dev' space
    tls:
    - hosts:
      - dev.bikesharingweb.nginx.MY_CUSTOM_DOMAIN
      secretName: dev-bikesharingweb-secret

gateway:
  ingress:
    annotations:
      kubernetes.io/ingress.class: nginx  # Custom Ingress
      cert-manager.io/cluster-issuer: letsencrypt
    hosts:
      - dev.gateway.nginx.MY_CUSTOM_DOMAIN  # Assumes deployment to the 'dev' space
    tls:
    - hosts:
      - dev.gateway.nginx.MY_CUSTOM_DOMAIN
      secretName: dev-gateway-secret
```

Voer een upgrade uit voor de voorbeeld toepassing met `helm` :

```console
helm upgrade bikesharingsampleapp . --namespace dev --atomic
```

Ga naar de voorbeeld toepassing in de *azureuser1 voor ontwikkel aars/* onderliggende ruimte en Let op dat u wordt omgeleid om HTTPS te gebruiken. U ziet ook dat de pagina wordt geladen, maar de browser bevat een aantal fouten. Wanneer u de browser console opent, wordt de fout weer gegeven in verband met een HTTPS-pagina voor het laden van HTTP-resources. Bijvoorbeeld:

```console
Mixed Content: The page at 'https://azureuser1.s.dev.bikesharingweb.nginx.MY_CUSTOM_DOMAIN/devsignin' was loaded over HTTPS, but requested an insecure resource 'http://azureuser1.s.dev.gateway.nginx.MY_CUSTOM_DOMAIN/api/user/allUsers'. This request has been blocked; the content must be served over HTTPS.
```

U kunt deze fout oplossen door [BikeSharingWeb/azds. yaml][azds-yaml] zoals hieronder te wijzigen:

```yaml
...
    ingress:
      annotations:
        kubernetes.io/ingress.class: nginx
        cert-manager.io/cluster-issuer: letsencrypt
      hosts:
      # This expands to [space.s.][rootSpace.]bikesharingweb.<random suffix>.<region>.azds.io
      - $(spacePrefix)$(rootSpacePrefix)bikesharingweb.nginx.MY_CUSTOM_DOMAIN
      tls:
      - hosts:
        - $(spacePrefix)$(rootSpacePrefix)bikesharingweb.nginx.MY_CUSTOM_DOMAIN
        secretName: dev-bikesharingweb-secret
...
```

[BikeSharingWeb/package.js][package-json] bijwerken met een afhankelijkheid van het *URL* -pakket.

```json
{
...
    "react-responsive": "^6.0.1",
    "universal-cookie": "^3.0.7",
    "url": "0.11.0"
  },
...
```

Werk de methode *getApiHostAsync* in [BikeSharingWeb/lib/helpers.js][helpers-js] bij voor het gebruik van https:

```javascript
...
    getApiHostAsync: async function() {
        const apiRequest = await fetch('/api/host');
        const data = await apiRequest.json();
        
        var urlapi = require('url');
        var url = urlapi.parse(data.apiHost);

        console.log('apiHost: ' + "https://"+url.host);
        return "https://"+url.host;
    },
...
```

Ga naar de `BikeSharingWeb` map en gebruik `azds up` om uw bijgewerkte *BikeSharingWeb* -service uit te voeren.

```console
cd ../BikeSharingWeb/
azds up
```

Ga naar de voorbeeld toepassing in de *azureuser1 voor ontwikkel aars/* onderliggende ruimte en Let op dat u wordt omgeleid om HTTPS zonder fouten te gebruiken.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe Azure Dev Spaces werkt.

> [!div class="nextstepaction"]
> [Hoe Azure Dev Spaces werkt](../how-dev-spaces-works.md)


[az-cli]: /cli/azure/install-azure-cli?view=azure-cli-latest
[az-aks-get-credentials]: /cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials
[az-network-dns-record-set-a-add-record]: /cli/azure/network/dns/record-set/a?view=azure-cli-latest#az-network-dns-record-set-a-add-record
[custom-domain]: ../../app-service/manage-custom-dns-buy-domain.md#buy-the-domain
[dns-zone]: ../../dns/dns-getstarted-cli.md
[azds-yaml]: https://github.com/Azure/dev-spaces/blob/master/samples/BikeSharingApp/BikeSharingWeb/azds.yaml
[azure-account-create]: https://azure.microsoft.com/free
[cert-manager]: https://cert-manager.io/
[helm-installed]: https://helm.sh/docs/intro/install/
[helm-stable-repo]: https://helm.sh/docs/intro/quickstart/#initialize-a-helm-chart-repository
[helpers-js]: https://github.com/Azure/dev-spaces/blob/master/samples/BikeSharingApp/BikeSharingWeb/lib/helpers.js#L7
[kubectl]: https://kubernetes.io/docs/user-guide/kubectl/
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[letsencrypt-staging-issuer]: https://cert-manager.io/docs/configuration/acme/#creating-a-basic-acme-issuer
[package-json]: https://github.com/Azure/dev-spaces/blob/master/samples/BikeSharingApp/BikeSharingWeb/package.json
[values-yaml]: https://github.com/Azure/dev-spaces/blob/master/samples/BikeSharingApp/charts/values.yaml
