<h1>DevOps Memoir</h1>

<h2>Kubernetes</h2>
<h2>Cluster Architecture</h2>
*Worker nodes: includes the kubelet and kube-proxy which are the container runtime engine ie. run containers Eg. Docker, rkt, containerD etc 
*Master nodes: includes the ETCD cluster, Kube Api-server, Kube controllee Manager and Kube scheduler
<h2>Docker-Vs-ContainerD</h2>
*Crictl is the CLI for containerD majorly a general purpolse CLI
<h3>Master Nodes</h3>
-ETCD: Is a Key-value store, stores data in rows and colums: stores information in pages within a file.There are various versions; v 0.1, 0.5,2.0, 3.1.
*NB With the release of version 3.4, the default API Version is set to 3.
*Default port of etcd is 2379.
-Kube Api-sever: Is the primary management component in K8S. Is the only component that interacts directly with the etcd controler store.
-Kube controler manager: Continuously monitors system to bring to full action according to the desire of the user. *watch status, remediate situation. *Types: Rplication controler, namespace controler, CronJob, Deplyment controlers. *These are all controled by the Kube Contoler manager, "Kube-controler-manager-service"
-Kube-Scheduler: Schedules pods on nodes: depending on the criteria.
*HOW? 
*It looks at each pod and determines what nodes are best for it.
*ie. filter nodes and Rank nodes
* Installing Kube-scheduler, "wget https://URL", install then run as service.
* To view Kube-scheduler option, "kubeadm", then run "cat/etc/kubernetes/manifests/kube-scheduler.yaml"
<h3>Worker Nodes</h3>
-Kubelet: Registers nodes with the cluster, creates pods, monitors nodes and pods.
*To view kubelet options, run "ps-aux | grep kubelet"
-Kube-proxy: It looks for new services in the k8s environment and create snodes to forward traffic to those services to the back end pods using IP tables Rules.
* Traffic from Service to pods through pod networking.
<h2>PODS</h2>
- Is the smallest unit of a kubernetes object , is a set of 1 or more containers deployed in a single node.
- A pod is a single instanve of an application.
- Is the smallest object you can create in K8S.
- In a pod, we also have helper containers (Replication containers, Replicasets) that is a copy of the original container just in caseit fails, now k8s helps to run these containers just in case it fails.
- K8s helps to run these containers/apps and groups them according to their use.
* When upscaling a pod, we do not increase the number of containers but increase the pods.
* When downsizing, we remove pods that are no longer required and not the container itself. 
*NB Nginx is used to set up a proxy-server, it receives a request, passes it to the proxied server, retrieves responses from them and sends them to the client.
<h2>Deployments</h2>
-This talks about how we deploy our application in a production environment.
-Deployment gives the capability to upgrade the underlying instances (pods) seamlessly using rolling updates, undo changes, pauses and resume changes as required.
-How do we create a deployment ?
* We draw same information in the file of the replicaset ie. the manifest. In this case the "kind will be deployment" 
* Run "kubectl create -f deployment-definition.yml"
* NB When finding it difficult to copy and paste yaml files directly to the vcs, use the "kubectl run" command.
* Create an NGINX Pod 
-kubectl run nginx --image=nginx
* Generate POD Manifest YAML file (-o yaml). Don’t create it(–dry-run)
-kubectl run nginx --image=nginx --dry-run=client -o yaml
*Create a deployment
-kubectl create deployment --image=nginx nginx
*Generate Deployment YAML file (-o yaml). Don’t create it(–dry-run)
-kubectl create deployment --image=nginx nginx --dry-run=client -o yaml
*Generate Deployment YAML file (-o yaml). Don’t create it(–dry-run) and save it to a file.
-kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml
*Make necessary changes to the file (for example, adding more replicas) and then create the deployment.
-kubectl create -f nginx-deployment.yaml
*OR
*In k8s version 1.19+, we can specify the –replicas option to create a deployment with 4 replicas.
*kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml
<h3>Common errors</h3>
* It is important to note that there may be errors when trying to create a deployment.
* "Kind" is case sensitive and the description should start with an upper case.
- to edit a deployment file for instance , run " vi deployment file"
