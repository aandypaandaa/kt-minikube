# Minikube kt

## Описание проекта

Этот проект демонстрирует процесс развертывания Minikube, создание Pod из YAML манифеста и работу с Pod Redis в Kubernetes. Все шаги документированы для выполнения на локальном компьютере или виртуальной машине.

## Шаг 1: Развертывание Minikube

### Установка Minikube

1. Следуйте инструкциям на официальном сайте для установки Minikube: [Minikube Installation Guide](https://minikube.sigs.k8s.io/docs/start/).

2. Запустите Minikube:
   ```bash
   minikube start
   ```

## Шаг 2: Создание и развертывание Pod

### Создание файла pod.yaml

Создайте файл `pod.yaml` и добавьте в него следующий манифест:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-nginx
spec:
  containers:
  - name: nginx-container
    image: nginx:1.10
```

### Развертывание Pod

1. Примените манифест для создания Pod:
   ```bash
   kubectl create -f pod.yaml
   ```

2. Если возникнет ошибка, проверьте синтаксис файла и убедитесь, что структура манифеста корректна. Для валидации используйте команду:
   ```bash
   kubectl apply -f pod.yaml --validate=true
   ```

## Шаг 3: Работа с Pod Redis

### Запуск Pod Redis

1. Запустите Pod Redis:
   ```bash
   kubectl run redis --image=redis:5.0 -n default
   ```

2. Проверьте, что Redis запустился и находится в статусе Running:
   ```bash
   kubectl get pods -n default
   ```

3. Убедитесь, что версия Docker image — redis:5.0:
   ```bash
   kubectl get pod redis -n default -o jsonpath="{..image}"
   ```

4. Отредактируйте Pod Redis, чтобы изменить версию Docker image на redis:6.0:
   - Откройте Pod для редактирования:
     ```bash
     kubectl edit pod redis -n default
     ```
   - Измените строку `image: redis:5.0` на `image: redis:6.0`.
   - Сохраните изменения и закройте редактор.

5. Проверьте логи контейнера:
   ```bash
   kubectl logs redis -n default
   ```

