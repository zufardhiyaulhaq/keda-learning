# HTTP Scaler

this HTTP scaler can scale from 0 if there is any traffic, but the first X seconds of traffic will be delayed because cold start (similar like KNative serving). It's using experimental KEDA HTTP addon https://kedacore.github.io/http-add-on/ with additional CRDs called HTTPScaledObject

1. Create the deployment & service
```
kubectl apply -f nginx.yaml

➜  http git:(main) ✗ k get pod 
NAME                              READY   STATUS    RESTARTS   AGE
nginx-deployment-96b9d695-2d4c8   1/1     Running   0          40s
(⎈|main-ps-sy-id-s-01:keda-testing) [30/12/25 | 8:59:39]
➜  http git:(main) ✗ k get service
NAME            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
nginx-service   ClusterIP   172.16.10.126   <none>        8080/TCP   7s
(⎈|main-ps-sy-id-s-01:keda-testing) [30/12/25 | 8:59:42]
➜  http git:(main) ✗ k get endpointslice
NAME                  ADDRESSTYPE   PORTS   ENDPOINTS        AGE
nginx-service-slvm2   IPv4          80      192.168.154.87   23s
```

to only scale the services when there is traffic, we will create HTTPScaledObject

