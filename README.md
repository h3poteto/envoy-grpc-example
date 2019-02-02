# envoy-grpc-example
## Prepare
### kubernetes
You have to prepare kubernetes cluster. I'm using EKS on AWS.

## Run
```bash
$ kubectl apply -f namespace.yml
$ kubectl apply -f envoy-configmap.yml
$ kubectl apply -f deployment-backend.yml
$ kubectl apply -f service.yml
$ kubectl apply -f deployment-client.yml
```

```bash
$ kubectl get pods -n envoy-grpc-example
NAME                                      READY   STATUS    RESTARTS   AGE
grpc-client-deployment-fdf54c64b-xxtjz    2/2     Running   0          7s
grpc-server-deployment-57699fcb78-n7mr5   2/2     Running   0          1m
grpc-server-deployment-57699fcb78-nv9dc   2/2     Running   0          1m
[akira]:~/src/github.com/h3poteto/envoy-grpc-example
$ kubectl logs -f grpc-client-deployment-fdf54c64b-xxtjz -n envoy-grpc-example -c client
People are added
Name Ryoko Shintani, Age: 37
Name Aoi Yuuki, Age: 26
Name Yui Horie, Age: 42
Name Kana Hanazawa, Age: 29
Name Ayana Taketatsu, Age: 29
-------------------------------------------------------------
Name Kana Asumi, Age: 35
Name Ayane Sakura, Age: 25
Name Yuuko Goto, Age: 43
Name Yukari Tamura, Age: 42
Name Yuka Iguchi, Age: 30
Name Yoko Hikasa, Age: 33
-------------------------------------------------------------
$ kubectl logs -f grpc-server-deployment-57699fcb78-n7mr5  -n envoy-grpc-example -c python
Starting server...
Listen :50051
Person added: {'name': 'Ryoko Shintani', 'age': 37, 'tags': []}
Person added: {'name': 'Aoi Yuuki', 'age': 26, 'tags': []}
Person added: {'name': 'Yui Horie', 'age': 42, 'tags': []}
Person added: {'name': 'Kana Hanazawa', 'age': 29, 'tags': []}
Person added: {'name': 'Ayana Taketatsu', 'age': 29, 'tags': []}
[{'name': 'Ryoko Shintani', 'age': 37, 'tags': []}, {'name': 'Aoi Yuuki', 'age': 26, 'tags': []}, {'name': 'Yui Horie', 'age': 42, 'tags': []}, {'name': 'Kana Hanazawa', 'age': 29, 'tags': []}, {'name': 'Ayana Taketatsu', 'age': 29, 'tags': []}]
[{'name': 'Ryoko Shintani', 'age': 37, 'tags': []}, {'name': 'Aoi Yuuki', 'age': 26, 'tags': []}, {'name': 'Yui Horie', 'age': 42, 'tags': []}, {'name': 'Kana Hanazawa', 'age': 29, 'tags': []}, {'name': 'Ayana Taketatsu', 'age': 29, 'tags': []}]
[{'name': 'Ryoko Shintani', 'age': 37, 'tags': []}, {'name': 'Aoi Yuuki', 'age': 26, 'tags': []}, {'name': 'Yui Horie', 'age': 42, 'tags': []}, {'name': 'Kana Hanazawa', 'age': 29, 'tags': []}, {'name': 'Ayana Taketatsu', 'age': 29, 'tags': []}]
```
