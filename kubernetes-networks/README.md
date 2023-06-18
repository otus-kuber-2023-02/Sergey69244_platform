## Домашняя работа 3 (kubernetes networks)

1. Добавлены readness и liveness пробы в kubernetes-intro/web-pod.yml
2. Создан Deployment web-deploy.yaml
3  Добавление сервисов в кластер ( ClusterIP ) web-svc-cip.yaml
4. Включен режим балансировки IPVS
5. Установлен MetalLB v 0.9.6 в Layer2-режиме, исправлены манифесты
6. Добавлен сервиса LoadBalancer web-svc-lb.yaml
7. Установлен Ingress-контроллер и прокси ingress-nginx
8. Созданы правила Ingress, манифест исправлен под новую версию, web-ingress.yaml
