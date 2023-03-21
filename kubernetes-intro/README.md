## Домашняя работа #1 

### Разберитесь почему все pod в namespace kube-system восстановились после удаления.
kubelet запущен как сервис systemd. Он занимается процессом запуска pod'ов.
Все pod'ы кроме core-dns - это статические pod, управляемые напрямую kubelet
Их описание хранится в /etc/kubernetes/manifests/
core-dns - запускается deployment с replicaset 2

### Запуск pod
Создан web сервер на основе образа nginx-alpine, контейнер залит на Docker Hub sergey69244/webserver:0.1

Создан файл манифеста и запущен под. Пробрасываем подключение к поду и убеждаемся в его работоспособности
```
kubectl port-forward --address 0.0.0.0 pod/web 8000:8000
```

Проверить раюоту можно командой
```
curl -s http://localhost:8000/index.html
```

### Hipster shop
Создан контейнер frontend и залит на Docker Hub sergey69244/frontend:0.1

Создан файл описания пода с помощью команды
```
kubectl run frontend --image sergey69244/frontend:0.1 --restart=Never --dry-run -o yaml > frontend-pod.yaml
```
### Hipster shop | Задание со *
Под не запускался из-за отсутсвия переменных окружения (env)