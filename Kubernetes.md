1. [Базові знання](#Базові знання)

## Базові знання

1. Основний компонент k8s - це кластер.
2. Кластер складається з node.
3. Ноди є одвух типів: **master node** та **worker node**.
4. Master node відповідає за керування кластером, worker node відповідає за виконання задач.
Worker node - сервер на якому запускаються і працюють контейнери.
Master node - сервер який керує Worker node.
Всі команди управління посилаються на Master node.


[Детально про node:](https://kubernetes.io/docs/concepts/architecture/nodes/)
Master node складається з таких компонентів:
    - **API server** - це основний компонент, який використовується для взаємодії з кластером.
    - **etcd** - це key-value база даних, яка використовується для зберігання конфігурації кластера.
    - **scheduler** - це компонент, який відповідає за розподіл задач по worker node.
    - **controller manager** - це компонент, який відповідає за виконання додаткових функцій, таких як: контроль стану, розподіл ресурсів, контроль доступу та інші.
Worker node складається з таких компонентів:
    - **kubelet** - це основний компонент, який відповідає за виконання задач на ноді.
    - **kube-proxy** - це компонент, який відповідає за мережеве взаємодію між нодами.
    - **container runtime** - це компонент, який відповідає за запуск контейнерів.

Kubernetes cluster повинен складатись як мінімум з 1 master node та 1 worker node.

## [Чому потрібен Kubernetes:](https://kubernetes.io/uk/docs/concepts/overview/what-is-kubernetes/#%D1%87%D0%BE%D0%BC%D1%83-%D0%B2%D0%B0%D0%BC-%D0%BF%D0%BE%D1%82%D1%80%D1%96%D0%B1%D0%B5%D0%BD-kubernetes-%D1%96-%D1%89%D0%BE-%D0%B2%D1%96%D0%BD-%D0%BC%D0%BE%D0%B6%D0%B5-%D1%80%D0%BE%D0%B1%D0%B8%D1%82%D0%B8)
## Чому Kubernetes популярний:
1. service discovery - можливість відстежувати стан сервісів.
2. load balancing - можливість розподіляти навантаження між сервісами.
3. storage orchestration - можливість автоматично створювати та видаляти зберігання для контейнерів.
4. automated rollouts and rollbacks - можливість автоматично розгортати та відкочувати оновлення.
5. automatic bin packing - можливість автоматично розподіляти ресурси між контейнерами.
6. self-healing - можливість автоматично перезапускати контейнери, які зупинилися.
7. secret and configuration management - можливість керувати конфігурацією та секретами.

## [Головні об'єкти Kubernetes:](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)
1. **Pod** - це найменша одиниця в Kubernetes. Він є логічною групою контейнерів, які завжди працюють разом.
2. **Deployment** - це об'єкт, який використовується для опису стану вашого додатку. Він складається з одного або декількох Pod.
3. **Service** - це об'єкт, який використовується для доступу до вашого додатку. Він використовується для виконання балансування навантаження між Pod. 
4. **Node** - це об'єкт, який представляє собою один фізичний або віртуальний сервер в кластері.
5. **Cluster** - це об'єкт, який представляє собою набір Node, які використовуються для запуску вашого додатку.
6. **Namespace** - це об'єкт, який використовується для групування іменованих ресурсів в кластері.
7. **Volume** - це об'єкт, який використовується для зберігання даних, які можуть бути доступні для контейнерів в Pod.
8. **ConfigMap** - це об'єкт, який використовується для зберігання конфігурації, яка може бути доступна для контейнерів в Pod.
9. **Secret** - це об'єкт, який використовується для зберігання секретів, які можуть бути доступні для контейнерів в Pod.
10. **Ingress** - це об'єкт, який використовується для доступу до вашого додатку ззовні кластера.
11. **StatefulSet** - це об'єкт, який використовується для запуску декількох однакових Pod, які мають стан.
12. **DaemonSet** - це об'єкт, який використовується для запуску декількох однакових Pod на кожній Node.

Як правило в 1 pod запускається 1 контейнер. Так роблять для ліпшого масштабування. 
Autoscalingом займається Deployment. 
Deployment відповідає за запуск Pod і відслідковує їх стан, а також займається оновленням Pod.
Також Deployment може використовувати ReplicaSet, який відповідає за кількість Pod, які мають бути запущені. 
Можна встановити мінімальну та максимальну кількість Pod, які мають бути запущені.
Це як реплікація, але з можливістю оновлення. Схоже на docker-compose, але для Kubernetes.


## Команди для роботи з pod використовуючи cubeclt
```bash
kubectl run pod-name --image=httpd:2.4-alpine --port=80 --restart=Never  #створити pod
kubectl delete pods pod-name #видалити pod
kubectl get pods #переглянути список pod
kubectl describe pods pod-name #переглянути детальну інформацію про pod
kubectl logs pod-name #переглянути логи pod

kubectl exec pod-name -- ls /usr/local/apache2/htdocs/ #виконати команду в pod
kubectl exec -it pod-name -- /bin/sh #виконати команду в pod
kubectl port-forward pod-name 8888:80 #прокинути порт
```
## Створення deployment викоритовуючи cubeclt
```bash
kubectl create deployment deployment-name --image=httpd:2.4-alpine --port=80
```
## Створення service викоритовуючи cubeclt
```bash
kubectl expose deployment deployment-name --type=NodePort --port=80
```
## Основні команди для роботи з kubectl
```
kubectl get - відобразити список ресурсів
kubectl get nodes - відобразити список Node'ів
kubectl describe - показати детальну інформацію про ресурс
kubectl describe nodes - показати детальну інформацію про Node'и
kubectl describe pods - показати детальну інформацію про Pod'и
kubectl logs - вивести логи контейнера, розміщеного в Pod'і
kubectl exec - виконати команду в контейнері, розміщеному в Pod'і
kubectl delete - видалити ресурс

kubectl get deployments - відобразити список Deployment'ів
kubectl create deployment - створити Deployment 
kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1 - створити Deployment з ім'ям kubernetes-bootcamp і образом gcr.io/google-samples/kubernetes-bootcamp:v1
```
## Manifest файл
Зазвичай використовують manifest файл для опису ресурсів. 
```yml
#pod.yml
apiVersion: v1
kind: Pod #тип ресурсу
metadata: #метадані
  name: pod-name #ім'я ресурсу
  labels: #мітки
    app: app-name #мітка app зі значенням app-name, яка буде використовуватися для пошуку ресурсу
spec:
  containers:
    - name: container-name
      image: httpd:2.4-alpine
      ports:
        - containerPort: 80
```
В середині маніфест файлу можна змінювати image без перезапуску pod для оновлення контейнера.
```yml
#pod.yml
apiVersion: v1
kind: Pod #тип ресурсу
metadata: #метадані
  name: pod-name #ім'я ресурсу
  labels:
    app: app-name 
spec:
  containers:
    - name: container-name
      image: nginx:alpine3.17-slim
      ports:
        - containerPort: 80
```

**Запуск pod з manifest файлу**
```bash
kubectl apply -f pod.yml
```

## Deployments
```bash
kubectl get deployments #переглянути список deployments
kubectl describe deployments #переглянути детальну інформацію про deployments
kubectl get replicaset #переглянути список replicaset
kubectl describe replicaset #переглянути детальну інформацію про replicaset
```
## Deployment commands:  
```bash
kubectl create deployment deployment-name --image=httpd:2.4-alpine --port=80 #створити deployment
kubectl scale deployment deployment-name --replicas=3 #змінити кількість реплік 
kubectl delete deployment deployment-name #видалити deployment
kubectl autoscale deployment deployment-name --min=3 --max=5 --cpu-percent=80 #встановити автоматичне масштабування
kubectl set image deployment deployment-name httpd=nginx:alpine3.17-slim #оновити image
kubectl rollout undo deployment deployment-name #відкатити оновлення на попередню версію
kubectl rollout undo deployment deployment-name --to-revision=1 #відкатити оновлення на певну версію,
# версію можна переглянути за допомогою команди kubectl rollout history deployment deployment-name
kubectl rollout restart deployment deployment-name #перезапустити deployment
# використовується для оновлення конфігурації deployment, наприклад, якщо ви змінили image в deployment,
# то використовуючи цю команду ви перезапустите deployment 
# з image останньої версії тегу(коли назва та тег image не змінилася, але він оновився)


kubectl get hpa #переглянути список autoscaling
kubectl describe deployment deployment-name #переглянути детальну інформацію про deployment
kubectl get rs #переглянути список replicaset 
kubectl describe rs #переглянути детальну інформацію про replicaset
kubectl rollout status deployment deployment-name #перевірити статус оновлення deployment
kubectl rollout history deployment deployment-name #переглянути історію оновлень deployment
```   

## Створення deployment використовуючи manifest файл
```yml
#deployment.yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-name
  labels:
    app: app-name
spec:
  replicas: 3 #кількість реплік
  selector: #вибірка pod'ів, які будуть контролюватися deployment
    matchLabels: #вибірка за міткою app зі значенням app-name
      app: app-name
  template:
    metadata:
      labels: #мітки, які будуть використовуватися для пошуку pod'ів,
        #мають співпадати з мітками вибірки selector
        app: app-name
    spec:
      containers:
        - name: container-name
          image: httpd:2.4-alpine
          ports:
            - containerPort: 80
```
**Запуск deployment з manifest файлу**
```bash
kubectl apply -f deployment.yml
```

В цьому файлі можна оновлювати image, після оновлення потрібно виконати команду:
```bash
kubectl apply -f deployment.yml
```

**Додавання autoscaling до deployment**
```yml
#deployment-replicas.yml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: hpa-name
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: deployment-name
  minReplicas: 2
  maxReplicas: 5
  metrics: #метрики, за якими відбувається масштабування
    - type: Resource #тип метрики
      resource: #ресурс, за яким відбувається масштабування
        name: cpu #тип ресурсу, в даному випадку відбувається масштабування за cpu
        target: #ціль, яку необхідно досягти
          type: Utilization #тип цілі
          averageUtilization: 50 #середнє значення використання ресурсу у %
    - type: Resource
      resource:
        name: memory
        target:
          type: Utilization
          averageUtilization: 80
```

**Запуск autoscaling з manifest файлу (потрібно запустити після deployment)**
Також можна прописати в manifest файлі deployment, щоб autoscaling запускався автоматично після створення deployment.
Для цього потрібно в deployment.yml додати наступний код, що розділить частину з autoscaling:
```yml
---
```
```bash
kubectl apply -f deployment-replicas.yml
```

## Services
**Зараз існує 4 типи сервісів:**
- ClusterIP - сервіс доступний лише в межах кластера
- NodePort - сервіс доступний ззовні кластера
- LoadBalancer - сервіс доступний ззовні кластера, використовується для роботи з балансувальниками навантаження(тільки для публічних хмар AWS, Azure, GCP)
- ExternalName - сервіс, який використовується для доступу до зовнішніх ресурсів

**Створення сервісу ClusterIP**
```bash
kubectl create service clusterip service-name --tcp=8080:80 #створити сервіс ClusterIP з нуля
kubectl expose deployment deployment-name --name=service-name --type=ClusterIP --port=8888 --target-port=80 #створити сервіс ClusterIP на основі deployment
# --port=8888 - Це порт, на який інші компоненти у вашому кластері будуть надсилати трафік, коли вони взаємодіють з вашим сервісом.
# --target-port=80 - Це порт на ваших подах (або іншому ресурсі, що виставляється), до якого сервіс буде перенаправляти вхідний трафік. Це порт, на якому ваше додаток слухає всередині поду.

kubectl apply -f project/curl-pod.yml #створити pod
kubectl exec curl-pod -- curl http://1.1.1.1:8888 #перевірити доступність сервісу з pod'а

kubectl expose deployment deployment-name --type=NodePort --name=service-name --port=8888 --target-port=80
#створити сервіс NodePort на основі deployment
kubectl get svc #переглянути список сервісів, виведе порт, на який буде доступний сервіс
kubectl get nodes -o wide #переглянути список нод, виведе external ip ноди
# так як використовується Docker Desktop, то перенаправить на localhost:port

kubectl delete service service-name #видалити сервіс
kubectl get svc #переглянути список сервісів
```