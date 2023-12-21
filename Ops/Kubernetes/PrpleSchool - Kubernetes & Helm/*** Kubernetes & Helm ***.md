#### Kubernetes
- ready solution at cloud providers
- wider used
- easy scalability under load
- flexible update scenarios
#### Docker swarm
- native Docker solution
- easier setup

---

## SetUp
- Kubectl 
- VM driver (qemu)
- minikube

---

## Pod

- Kubernetes element
- abstraction over container
- has it's own IP
- can contains several containers

## Service

- provides continuous access to the container
- types of services:
	- NodePort - outside access by the port number
	- Ingress - access by the domain name
	- ClusterIp - access from other pods
	- LoadBalancer - outside access to one service 

---

## Master Node
- API Server / Auth
- Scheduler
- Controller Manager
- etcd (kv store)

---

## Aproaches

Imperative
- appropriate for single task
- appropriate for test
>Direct interaction with cluster
```bash
kubectl run nginx --image=nginx --restart=Never
```



Declarative
- Infrastructure as a code
- versioning
- better for work in team
> 1. Description in configuration
> 2. Run through kubectl
> 3. Modify and Delete configuration 
```yml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    env: test
spec:
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
  nodeSelector:
    diskType: ssd
```

---

## Yaml

```YAML
#Strings
name: App
name2: "App"
name3: 'App'

#Digit
version: 30
version: 1.2
version: 1.2.333

#Boolean
isDev: true
isDev2: on
isDev3: yes

#Arrays
users:
  - James
  - John
users2: ["John", "James"]

#Multiline
line: |
  Valid
  Multi
  Lines

#Singleline
line2: >
  Transform
  Into
  Single Line
```

---

## Configuration

Each configuration contains
- metadata
- spec

```YAML
apiVersion: v1
```

- v1
	- Pod
	- Event
	- Namespace
	- Service
	- configMap
	- other
- apps/v1
	- ControllerRevion
	- StatefullSet

---

## Running

```bash
kubectl apply -f .
kubectl get pods
kubectl get services
minikube ip
```


> Life cycle: Scheduled => Pull => Create => Start

```bash
kubectl describe pods <POD_NAME>
```

```shell
kubectl delete pod my-pod
```

---

## Deployments

> Deployment can manage several pods ant its configurations

```bash
kubectl apply -f app-deployment.yml
kubectl get all
```

Rollout

```
kubectl rollout history deployment short-app-deployment
kubectl set image deployment.apps/short-app-deployment \
short-app=antonlarichev/short-app:latest
kubectl rollout restart deployment short-app-deployment
```

---

## Ingress

Ingress controllers
- Nginx
- AWS
- GCP
- other

```shell
minikube addons list
minikube addons enable ingress
```

```bash
kubectl get ingress
```

---

## Port forwarding

```bash
kubectl port-forward pods/postgres-deployment-xxx 5432:5432
```

---

## Volume

- Volume - space (storage) inside the pod
- Persistent Volume - object (storage) outside the pod
- Persistent Volume Claim - claim to get volume (storage) for pod