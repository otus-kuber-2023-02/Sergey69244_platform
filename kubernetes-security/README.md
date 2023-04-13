## Домашняя работа #5 (kubernetes security)

## Task01:
 - Создан service account `bob` с ролью `admin` в кластере
 - Создан service account `dave` (по умолчанию прав в кластере нет)

## Task02:
 - Создан namespace `prometheus`
 - Создан service account `carol` в namespace `prometheus`
 - Создана роль `pod-reader` с verbs ["get", "list", "watch"] для `pod`
 - Создан role binding `pod-reader` с ссылкой на роль `pod-reader`

## Task03:
 - Создан namespace `dev`
 - Создан service account `jane` в namespace `dev`
 - Создан role binding в `dev` `jane-admin` связывающий service account `jane` и кластерную роль  `admin`
 - Создан service account `ken` в namespace `dev`
 - Создан role binding в `dev` `ken-view` связывающий service account `ken` и кластерную роль  `view`
