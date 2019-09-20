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

Mozemy zaopserwować stworzony service typu clusterIP który zapewni na dostep do dashborda  

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/traefik-web-ui.png)

<h3>kubectl get ingress -n kube-system</h3>

Mozemy zobaczyć na jakiego hosta zapinamy nasz dashbord

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/get-ingress.png)

<h3>edomin.pl</h3>

Tak wyglada nasz dashbord

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/edomin.pl.png)

<h3>kubectl apply -f cheese-deployments.yaml</h3>

Tworzymy deployment 3 prostych aplikacji którzy wystawiaja tylko jedna podstronę
kazdy depolyment zaweira 2 pody.
Tworze rowniez deploy nginix który wyswietla nazwe hostnama oraz adres ip poda  

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/cheese-deployments.yaml.png)

<h3>kubectl get deployment -n projekt</h3>

Mozemy zobaczy utworzone działajace depolymeny

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/getdeployment.png)

<h3>kubectl get pod -n projekt</h3>

Możemy zobaczyc działajace pody w namespaces projekcie  

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/getpodnprojekt.png)

<h3>kubectl apply -f cheese-services.yaml</h3>

Tworzymy service dla tych depolymentów

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/fcheese-services.yaml.png)

<h3>kubectl get svc -n projekt</h3>

Mozrmy zobaczyć wszystkie servicy który utworzyłem dla deploymentów

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/getsvcnprojekt.png)

<h3>kubectl apply -f cheeses-ingress.yaml</h3>

Tworze ingresa do service który pozwala dodac dla domeny edomin path dla poszczegolnych applikacji

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/cheeses-ingress.yaml.png)


<h3>kubectl describe ingress cheeses -n projekt</h3>

Sprawdzam konfiguracje ingresa pathy dla domeny edomin.pl

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/describeingresscheeses.png)

<h3>edomin.pl</h3>

Mozna teraz zobaczyć ze nasze usługi dodały się do naszego ingrsa i mozemy zobaczyc te aplikacje z pozimu dashborda

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/edominv2.png)

<h3>kubectl create namespace jenkins</h3>

Teraz zrobie depoly jeszcze jednej aplikacji tzn jenkina
zaczne od stworzenia własnego namespacesa

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/namespacejenkins.png)

<h3>kubectl apply -f jenkins-deploy.yaml</h3>

Tworze depoly jenkina z 1 podem oraz tworze service i nowa usługe ingres

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/jenkins-deploy.yaml.png)

<h3>kubectl get pod -n jenkins</h3>

Sprawdzam czy usługa juz wystartowała i czy działa poprawnie

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/podnjenkins.png)

<h3>kubectl get svc -n jenkins</h3>

Sprawdzam konfiguracje service mozemy zobaczyc ze jenkins działa na niestandardowym porcie 8080

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/svcnjenkins.png)

<h3>kubectl get ingress -n jenkins</h3>

Sprawdzam konfiguracje ingresa

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/ingressjenkins.png)

<h3>kubectl describe ingress -n jenkins</h3>

Widać ze ingres w tym przypadku działa inaczej niz w wczesniej wdrozonch aplikacjiach ponieważ tutaj ingres nie działa na pathie a na subdomenie

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/describeingress.png)

Sprawdzam czy ingres poprawnie sie zapioł dla aplikacji jenkins i czy widac ja z dashborda

<h3>edomin.pl</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/jenkinsedomin.png)

dodałem wpis do /etc/hosts
35.246.27.48  jenkins.edomin.pl


<h3>jenkins.edomin.pl</h3>

Zobacze czy strona wyswietla sie prawidłowo

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/jenkins.pl.png)


### Jak działa loudbalanser

Wykonuje polecenie curl z własnego pc na adress domeny edomin.pl aby zasymulować wywołoanie naszy aplikacji zapietych na roznych /patch

curl edomin.pl/nginx

Sprawdzam czy loudbalanser działa prawidłowo i czy działa runrobin. usługa nginix zwraca adres ip poda oraz hostname wiec nadaje sie idealnie do tego aby to sprawdzić

lynx http://edomin.pl/nginx

<h3>Pierwsza próba</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/ngnix1.png)

<h3>Druga próba</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/ngnix2.png)

Przesledze teraz droge jaka nasz komputer musi pokonać aby odpowiedziała mu aplikacja

domena edomin została zakupiona w home.pl i został tam utworzony rekord A dla adresu 35.246.27.48

adress 35.246.27.48 to adres loudbalansera utworzonego w google cloud

Widać na obrazku ze adres ten został zapiety dla trzech maszyn wirtualnych które tworza cluster kubernetesa.

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/35.246.27.48.png)

Teraz zaloguje sie do maszyny wirtualnej gke-standard-cluster-2-default-pool-7e1dffd4-8vc2 przez ssh , aby moc pokazać jak dalej wyglada droga naszego curla a adres curl edomin.pl/nginx

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/logowanie-ssh.png)

Aby uzyskać wiekszy dostep do dodatkowych narzedi takich jak tcpdump nalezy wykonoć polecenie /usr/bin/toolbox

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/toolbox.png)

Teraz mozemy zainstalowac tcpdumpa

apt update -y
apt install tcpdump -y

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/installtcpdump.png)

Wykonuje curla z gke-standard-cluster-2-default-pool-7e1dffd4-8vc2 	 na gke-standard-cluster-2-default-pool-7e1dffd4-jdfl 	 
curl 10.154.0.3:32708
w ten sposób pokazuje iz kiedy przejdziemy juz przez loudbalanser mamy utworzony NodeIp

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/curl10.54.0.3.png)

Usługa jest rowniez dostepna po przez adresy ip hosta oraz port nodaport który mozemy zobaczyc tutaj

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/describe-svc-traefik-ingres-controler.png)

Adresy ip prywatne hostów i publiczne

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/googcloudssh.png)


Odpalamyna hoscie gke-standard-cluster-2-default-pool-7e1dffd4-jdfl polecenie tcpdump -vvv -i eth0 src host 35.246.27.48 and port 80   
i widzimy ze publiczny adress przechodzi przez interfejs eth0

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/checkport.png)


<h3>tcpdump -vvv -i cbr0 port 80</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/checkport.png)

Teraz widać że jest uzywany ingress który rozrzuci nam ruch na rozne pody ingres wie do których serviców ma sie skietować


Zeby zobaczyc co dzieje sie dalej potrzebujemy wejsc to contenera z aplikacja

docker ps -a| grep nginx-hello

docker exec -it f281dfd6c9a7  sh
