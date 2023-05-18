# docker_kuber_practice

1. Билдим image ```docker build -t qwertyforce/server:1.0.0 --network host -t qwertyforce/server:latest server```  
2. Проверяем работоспособность ```docker run -ti --rm -p 8000:8000 --name server qwertyforce/server:1.0.0``` 
3. Пуш в docker hub ```docker push qwertyforce/server:1.0.0```
4. Применяем manifest ```kubectl apply --filename deployment.yaml --namespace default  ```
5. Проверяем, что все запустилось ```kubectl get deployments.apps web --namespace default```
6. Пробрасываем порт, проверяем через curl/browser что все работает ```kubectl port-forward deployment/web 8080:8000 --namespace default```

```
C:\github\docker_example>kubectl describe deployment web
Name:                   web
Namespace:              default
CreationTimestamp:      Thu, 18 May 2023 12:36:22 +0300
Labels:                 app=server
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=server
Replicas:               2 desired | 2 updated | 2 total | 2 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=server
  Containers:
   server:
    Image:        qwertyforce/server:1.0.0
    Port:         8000/TCP
    Host Port:    0/TCP
    Liveness:     http-get http://:8000/hello.html delay=3s timeout=1s period=3s #success=1 #failure=3
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   web-5c947b9fc8 (2/2 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  11m   deployment-controller  Scaled up replica set web-5c947b9fc8 to 2
```
