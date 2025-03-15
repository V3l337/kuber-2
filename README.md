
# Домашнее задание к занятию «Базовые объекты K8S»

## Задание 1. Создать Pod с именем hello-world

### Создать манифест (yaml-конфигурацию) Pod.
```yml
apiVersion: v1
kind: Pod
metadata:
  name: hello-world
spec:
  containers:
  - name: echoserver
    image: gcr.io/kubernetes-e2e-test-images/echoserver:2.2
    ports:
    - containerPort: 8080
```
Использовать image - `gcr.io/kubernetes-e2e-test-images/echoserver:2.2`.
Подключиться локально к Pod с помощью `kubectl port-forward` и вывести значение (curl или в браузере).

```sh
kubectl port-forward pod/hello-world 8080:8080 --address 0.0.0.0
```

![Подключиться локально к Pod с помощью kubectl port-forward и вывести значение (браузере)](https://github.com/user-attachments/assets/0fccd1e5-1f3f-455b-ae24-20a9e860317c)


## Задание 2. Создать Service и подключить его к Pod

### Создать Pod с именем netology-web.
```yml
apiVersion: v1
kind: Pod
metadata:
  labels:
    app: netology-web
  name: netology-web
spec:
  containers:
  - name: netology-web
    image: gcr.io/kubernetes-e2e-test-images/echoserver:2.2
    ports:
    - containerPort: 8080
```
Использовать image — `gcr.io/kubernetes-e2e-test-images/echoserver:2.2`.

### Создать Service с именем netology-svc и подключить к netology-web.
```yml
apiVersion: v1
kind: Service
metadata:
  name: netology-svc
spec:
  selector:
    app: netology-web
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
  type: ClusterIP
```

Подключиться локально к Service с помощью `kubectl port-forward` и вывести значение (curl или в браузере).

```sh
kubectl port-forward svc/netology-svc 8080:8080 --address 0.0.0.0
```

![Подключиться локально к Service с помощью kubectl port-forward и вывести значение (браузере)](https://github.com/user-attachments/assets/25480203-7a6c-4225-ab71-e91d7333a25c)
