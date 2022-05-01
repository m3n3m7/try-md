Kubernetes 

k8s main component.
-> pod 
- smallest unit of k8s 
- abstraction over container.
- usually 1 app per pod.
- each pod gets its own ip address.
- new ip address on re-creation.

-> service
- permenant ip
- life cycle of pod and service not connected.
-> ingress 
- if you want to request the database from outside you should use ingress to forward the request .

-> config map 
- external configuration of your application.

-> secret 
- like config map but use to store secret data. store in 64 base encoded.

-> deployment 
- is a blue print for the pod of the app. 
- you not work with pod you work with deplyment so you can controll how replica you want.
- database can't be replicated by deployment cuz it has a state.
- deplyment is an abstraction layer on the pod.
- used for stateless app.

-> statefull set 
- used to replica of database like mongo, mysql and elastic search.
- used for state app.
- it is tedius to work with database in k8s.

so it prefered to use database from outside k8s.
___ 
### K8S Architectur 
- every node has 2 pods.
- 3 process must be installed on each node.
     - container runtime like docker.
     - kubelet 
     - kube proxy ---> forward the request.

- worker node do the actual work. 
- master node is responsible for (schedule pod / restart pod / monitor / add new node).

- in master node there are 4 process 
   -  api server ---> cluster gateway / use in authentication.
   -  schedular ---> where to put the pod ( inteligent ).
   -  control manager ---> detect cluster state changes.
   -  etcd ---> key value store date --> cluster brain --> all things get update in etcd.
 
 #### note 
 - in very small cluster you have **_2_** master node and **_3_** worker node .



___
### what is the mini kube ?
- it  is local one node for testing it contain the master processes and node processes together.
- docker runtime pre installed.
- master processes like (etcd/APIserver/scheduler/controllermanager) / node processes like (kubelet/proxykube/containerruntime).
- minikubes creates virtualbox in your labtop / nodes run in this virtual box.
### what is  kube ctl?
- kubectl is the way that i can interact with the node in virtualbox to add pod and servises and so on .
- api server is the main entry point to deal with node virtual . so we can deal with it using **_using UI , CLI or  API_**.

#### Note 
- the **kubectl** is the tool to deal with _cloud cluster , hyprid cluster or mini kube cluster_.

you need to download 
 1 - minikube 
 2 - kubectl
 3 - hypervisor (virtualbox).
___
### commands to deal with minikube.
1- minikube start -vm-driver="what you user ". 
2- kubectl get nodes 
3- minikube status 
4- kubectl version

from here we will interact with minikube cluster by using kubectl .

minikube cli---> for starting and deleting the culuster .
kubectl cli ---> for configure the minikube cluster .

___ 

### Basic kubectl commands .

1- kubectl get nodes --> the nodes that found.
2- kubectl get pod.
3- kubectl get services. 

#### Note 
- when you work you work with *__deployment__*(the abstraction layer above pod) not with pod the smallest unit in k8s.

4- kubectl create deployment Name(nginx-depl) --image=nginx(from docker container).

#### Note
- between the pod and deployment there is a layer called replicaset.

5- kubectl get replicaset.

6- kubectl describe pod podname 

7- kubectl logs podname 

8- kubectl exec -it podname -- bin/bash --->use in the debbuging issue .

9- kubectl delete deployment deploymentname.

#### Note
- when you want to make so many attributes in the deployment you want to do in config file so by 

10- kubectl apply -f thenameoffile.yaml 

11- kbectl get pod -o wide --> to know more information like ip address.
___
### kuberenetes with yaml 
3 parts of configuration file structure .

apiversion:
kind:
part1-->metadata metadata:
part2-->specification spec:
attributes of specific is specific to kind.
part3---> is the status the etcd is the main brain of the k8s so it can help us in that.

template has it's own config file inside the config file so : 


___

the project demo webapp with database 
mongo express && mongo db 

write the deployment config file and to know the ports and other staff go to the docker file images to know.

---

K8S for new version .

kubectl -h .
