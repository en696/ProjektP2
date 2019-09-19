# ProjektP2

<h1>Instalacj oraz konfiguracja clastra</h1>

<h3>gcloud compute instances list</h3>
dzięki temu poleceniu możemy zobaczyć wszystkie nody które tworzy klaster kubernetesa i jakie adresy ip maja. każdy node ma adres publiczny dzięki czemu możemy się zalogować poprzez ssh do każdego noda z osobna

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/gcloudcoumpute.png)

<h3>kubectl get node</h3

Te polecenie rownież wylistuje nam nody ale te polecenie jest wbudowane w cluster kubernetesa
i pozwoli wyswietlić jak dawno node został dodany, jego status czy jest sprawny oraz wersje kubernetesa

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/getnode.png)


<h3>kubectl create namespace projekt</h3>

Stworzyłem nowy namespaces dla naszego projektu

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/namespaces-projekt.jpg)

#dopisac

<h3>kubectl apply -f traefik-rbac.yaml</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/rbc.png)

<h3>kubectl get secret traefik-ingress-controller-token-cftk6</h3>

#dopisac

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/traefik-ingress-controller-token-cftk6.png)

<h3>kubectl apply -f traefik-ingress-controller.yaml</h3>

Stworzyłem ingres kontroler który zawiera Service i Deployment i znajduje sie w namespace kube-system dla wiekszego bezpieczenstwa aby zwykły urzytkownik nie mógł go skasować.
Jako ingres kontrolera uzyłem traefika.
Kontener wystawia dwa porty 80 do usług http oraz 8080 do zarzadzania do dashborda
Tworzymy usługe typu loadbalanser

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/traefik-ingress-controller.png)

<h3>kubectl get svc traefik-ingress-service -n kube-system</h3>

Sprawdzamy usługe loadbalanser . która została utworzona przez google cloud mozemy zobaczyć adres publiczny takiej usługi
Jak widzimy utworzenie servica typu loudbalanser automatycznie utwoczyło cluster IP oraz zmapowało porty do usługi

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/get_svc_traefik-ingress-service.png)

<h3>kubectl describe svc traefik-ingress-service -n kube-system</h3>

Możemy zobaczyc bardziej szczegółowe informacje odnosnie loaudbalansera

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/describe-svc-traefik-ingres-controler.png)

<h3>kubectl get serviceaccount traefik-ingress-controller -n  kube-system</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/serviceaccount-traefik-ingress-controller.png)

<h3>kubectl get pod -n kube-system | grep traefik</h3>

Możemy zobaczyć działajacego poda z ingrescontrolerem

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/grep-traefik.png)

<h3>kubectl describe  pod  traefik-ingress-controller-8c8b85bbc-hqpf4 -n kube-system</h3>

Możemy zobaczyć wiecej szczegłow o podzie i zobaczyc jego adres wewnetrzny

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/traefik-ingress-controller-8c8b85bbc-hqpf4.png)

<h3>kubectl apply -f ui.yaml</h3>

Tworze ingresa oraz service dla dashborda 

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/ui.yaml.png)

<h3>kubectl get svc traefik-web-ui -n kube-system</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/traefik-web-ui.png)

<h3>kubectl get ingress -n kube-system</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/get-ingress.png)

<h3>edomin.pl</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/edomin.pl.png)

<h3>kubectl apply -f cheese-deployments.yaml</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/cheese-deployments.yaml.png)

<h3>kubectl get deployment -n projekt</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/getdeployment.png)

<h3>kubectl get pod -n projekt</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/getpodnprojekt.png)

<h3>kubectl apply -f cheese-services.yaml</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/fcheese-services.yaml.png)

<h3>kubectl get svc -n projekt</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/getsvcnprojekt.png)

<h3>kubectl apply -f cheeses-ingress.yaml</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/cheeses-ingress.yaml.png)

<h3>kubectl get ingress -n projekt</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/get-ingress.png)

<h3>kubectl describe ingress cheeses -n projekt</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/describeingresscheeses.png)

<h3>edomin.pl</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/edominv2.png)

<h3>kubectl create namespace jenkins</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/namespacejenkins.png)

<h3>kubectl apply -f jenkins-deploy.yaml</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/jenkins-deploy.yaml.png)

<h3>kubectl get pod -n jenkins</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/podnjenkins.png)

<h3>kubectl get svc -n jenkins</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/svcnjenkins.png)

<h3>kubectl get ingress -n jenkins</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/ingressjenkins.png)

<h3>kubectl describe ingress -n jenkins</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/describeingress.png)

<h3>edomin.pl</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/jenkinsedomin.png)

dodałem wpis do /etc/hosts
35.246.27.48  jenkins.edomin.pl

<h3>jenkins.edomin.pl</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/jenkins.pl.png)
