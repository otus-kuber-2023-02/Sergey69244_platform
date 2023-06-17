## Домашняя работа #7 (kubernetes operator)

Работа проводилась в minikube v1.30.1

## Оператор

1. Созданы манифесты deploy/cr.yml и deploy/crd.yml, в crd добавлен openAPIV3Schema

## Контроллер

2. Создан контроллер build/mysql-operator.py Исправлено:
2.1 Добавлен параметр size в pv и pvc для backup
2.2 StorageClass заменен на manual, т.к. по default в minikube отрабатывает свой провижинер
2.3 pv для mysql удаляется непосредственно, а не через addopt, т.к. ему не назначен namespace и удаления не происходит
2.4 При загрузке манифестов добавлен параметр yaml.LoadSafe

## Deploy

3. Контроллер упакован в контейнер sergey69244/mysql-operator:v0.0.2
4. Создан deploymetn, service-account и роли

## Проверка

```
sergey@dev-minikube2:~/Sergey69244_platform/kubernetes-operators$ kubectl get jobs
NAME                         COMPLETIONS   DURATION   AGE
backup-mysql-instance-job    1/1           7s         13m
restore-mysql-instance-job   1/1           59s        3m37s
sergey@dev-minikube2:~/Sergey69244_platform/kubernetes-operators$ cat ./get_data.sh
#!/bin/bash

MYSQLPOD=$(kubectl get pods -l app=mysql-instance -o jsonpath="{.items[*].metadata.name}")

kubectl exec -it $MYSQLPOD -- mysql -potuspassword -e "select * from test;" otus-database

sergey@dev-minikube2:~/Sergey69244_platform/kubernetes-operators$ ./get_data.sh
mysql: [Warning] Using a password on the command line interface can be insecure.
+----+-------------+
| id | name        |
+----+-------------+
|  1 | some data   |
|  2 | some data-2 |
+----+-------------+
sergey@dev-minikube2:~/Sergey69244_platform/kubernetes-operators$


```