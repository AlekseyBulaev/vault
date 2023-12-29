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

Rollout (works only with deployments)

```
kubectl rollout history deployment short-app-deployment
kubectl set image deployment.apps/short-app-deployment \
short-app=antonlarichev/short-app:latest
kubectl rollout restart deployment short-app-deployment

kubectl rollout status deployment short-api-deployment --to-revision=2
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

Access Modes
- ReadWriteOnce - can be used by only one instance
- ReadOnlyMany - can be read by many instances
- ReadWriteMany - can be used by many instances

---

## StorageClass

```bash
kubectl get storageclasses.storage.k8s.io
```

- NAME - name of the storage class
- PROVISIONER - who manages the persistence (plugin)
- RECLAIMPOLICY - (retain, delete, ...) what to do when PVC is deleted
- VOLUMEBINDINGMODE - when allocate the storage
- ALLOWVOLUMEEXPANSION - can we expand the storage

```bash
kubectl apply -f postgres-pvc.yml
kubectl apply -f postgres-deplyment.yml
kubectl get pods
```

---

## Secrets

```bash
kubectl create secret generic pg-secret --from-literal PASSWORD=my_pass
kubectl get secrets
kubectl describe secrets pg-secret
```

```bash
kubectl get secrets pg-secret --template={{.data.PASSWORD}}
```

---

Helm

```bash
helm create short-service
```

 Logs

```bash
kubectl logs pods/<POD_NAME>
```

Dashboard

```bash
minikube dashboard
```

---

```bash
kubectl exec -it short-api-deployment-xxx -- /bin/bash
```

![[Pasted image 20231224204115.png]]

---

## ConfigMap

![[Pasted image 20231224204313.png]]

```bash
kubectl apply -f demo-config.yml
```

---

## HealthCheck

![[Pasted image 20231224210025.png]]

---

## NameSpace

```bash
kubectl get namespaces
kubectl config set-context --current --namespace=kubernates-dashboard
```

- separate app zones
- avoidance of naming conflicts
- dev / prod environments
- separate resources

```bash
kubectl api-resources --namespaced=false
```

---

## Helm

- declarative way
- package manager
- rollback and watch
- plugins

Components of Helm
1. Chart - A package containing descriptions of resources required for operation.
2. Repository - share published charts
3. Release - chart example works in kubernetes cluster

Chart contains of:
- Meta Data
- Values
- Templates

---

![[Pasted image 20231224223327.png]]


```bash
helm repo list
helm repo add stable htpps://charts.helm.sh/stable
helm repo update

helm install stable/mysql --generate-name
helm show chart stable/mysql
```

---

```bash
helm install short-service-release short-service
```

- Release - release info
- Values - parameters from values.yml
- Chart - data from chart.yml
- File - file access except default files
- Capabilities - cluster information
- Template - current template information

example:
![[Pasted image 20231226223154.png]]

---


```bash
helm ls

helm upgrade short-service-release ./short-service

helm install --debug --dry-run short-service-release ./short-service

#Create package
helm package ../short-service

helm repo index .

#check the release
helm lint short-service
helm template test ./short-service
helm get all

#testing
helm test short-app-release
```

---

## Work with secrets

```bash
helm plugin install https://github.com/jkroepke/helm-secrets --version v4.5.1
```