# ProjektP2

<h3>kubectl create namespace projekt</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/namespaces-projekt.jpg)

<h3>kubectl apply -f traefik-rbac.yaml</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/rbc.png)

<h3>kubectl get secret traefik-ingress-controller-token-cftk6</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/traefik-ingress-controller-token-cftk6.png)

<h3>kubectl apply -f traefik-ingress-controller.yaml</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/traefik-ingress-controller.png)

<h3>kubectl get svc traefik-ingress-service -n kube-system</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/get_svc_traefik-ingress-service.png)

<h3>kubectl describe svc traefik-ingress-service -n kube-system</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/describe-svc-traefik-ingres-controler.png)

<h3>kubectl get serviceaccount traefik-ingress-controller -n  kube-system</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/serviceaccount-traefik-ingress-controller.png)

<h3>kubectl get pod -n kube-system | grep traefik</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/grep-traefik.png)

<h3>kubectl describe  pod  traefik-ingress-controller-8c8b85bbc-hqpf4 -n kube-system</h3>

![Diagram](https://github.com/en696/ProjektP2/blob/master/obrazki/grep-traefik.png)

<h3>kubectl apply -f ui.yaml</h3>


<h3>kubectl get svc traefik-web-ui -n kube-system</h3>


<h3>kubectl get ingress -n kube-system</h3>
