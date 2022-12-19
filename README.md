# K8S
* # OverView:
  * Developed by Google.
* # Container:
  * Isolated environment which has own process, networking and it is like VM except it shares common resources like OS and OS kernel. 
  * OS Kernel which communicate with hardware system and container.
  * It is an environment which helps to run a image
  * Container is light weight
  * ## Fundamentals:
   * Compatibility with any OS
   * Less time to set up docker environment for new developer.
* # Image:
 * Package of application which have required software and dependency to run a application
* # Orchestration
	* Make a connectivity between the container
	* Scale up and scale down the container based on the load
	* Monitoring container health & performance
	* Above mentioned process automatically deploying and managing is known as Orchestration
	* ### Tools Available:
		* Docker swarm
		* Kubernetes - Google
		* MESOS - Apache
* # Kubernetes:
	* Supported by all cloud service providers such as Azure, AWS, 
	* High availability
	* Scale up & scale down
* # Architecture:
	### Worker Node: (Miniors)
	* It is a machine on which K8S installed on it.  Node may be a physical Machine / Virtual Machine.
	* Our application runs on this
	* Kubelet works in each node
	### Cluster:
	* It has more than 1 node and group together
	### Master Node:
	* It is nothing but a Node on which K8S installed on it and marked as Master.
	* kube-apiserver runs in the master node
	<img width="442" alt="image" src="https://user-images.githubusercontent.com/10528013/194047462-635e4c87-47ae-4991-a8a2-fcb7608a4f85.png">
	
	* ### Kubectl: - Kube command line tool / Kubecontrol:
		* kubectl run application_name 
	 		* helps to deploy the application on cluster
		* kubectl cluster-info
	 		* Helps to find cluster info
		* kubectl get nodes
			 * Helps to get all nodes
* # How to set a clustor in a machine?
	* Normally if we want to run K8s cluster, we have to install required components in Master Node (kubelet-apiserver, controller, etcd,...) as well as Worker Node (Container Runtime - to run an application, kubelet)
 * ## minikube
 	* It is a predifined all above components in a single machine and provide a single node K8S cluster. And it is available as a image.
 * ## kubeadm
 	* Do set up multi cluster K8S node in a machine
 * ## microK8s
 * ## Installation:
 	* Kubectl
	* Minikube
* ## Kubernetes:
	* Continer archestration platform
	* ### Pods:
		* Pods are a kubernetes object.
		* Container is not deployed seperately in K8S clustor node. which will be encapsulated with K8S object called POD.
		* Each POD has only one container will be deployed. And we can deploy more than one container but this is not a standard.
		* Each POD will have unique IP address.
		* ### yml file structure in K8S
		* ### Sample pod-definition.yml file
		* <img width="657" alt="image" src="https://user-images.githubusercontent.com/10528013/201673909-46a7d3f2-4625-4d98-b03a-d07660c8b086.png">
	* ### Replication Controller vs Replica Set:
		* Used to manage the POD life cycle which make sure that specified (replicas ) no of pod is runing 
		* Based on replicas defined in the file, replication controller/Replica set make sure pods running always
		* Replica set - newest one. Replication controller - older one
	* ### Replication Controller / Replica set:
		* Sample file
		* <img width="764" alt="image" src="https://user-images.githubusercontent.com/10528013/201679528-0f1d378d-8d16-4fff-8ca4-9784a0dd8b1c.png">
		* <img width="479" alt="image" src="https://user-images.githubusercontent.com/10528013/207301912-4f3f37ce-c3c5-4fd8-a663-e22a95f9b48c.png">
		* Selector section used to group the existing running pod using by their labels.
		* With the help of selector & labels replica set monitor group of pod instances ( manages the group of similar pod instances).

	* ### Command
		* ## Create Pod / (Replication controller / replica set)
			kubectl create -f fileName of Pod / (replica controller / replica set)
			kubectl create -f pod-definition.yml
			kubectl create -f replicaset-definition.yml
			kubectl create -f deployment-definition.yml
		* ## See the created pod / (Replication controller / replica set)
			kubectl get pods / (replicaset / replicationcontroller - rs) / deployments
		* ## Get Pod / replica set / deployment details more
			kubectl describe pod/replicaSet/deployment pod_name/replicaSet_name/deployment_name
		* ## Update the defintion file
			kubectl apply -f deployment-definition.yml/replicaset-definition.yml/pod-definition.yml
		* ## RollOut
			kubectl rollout undo/status/history deployment_name
		* ## Scale the pod using command
			3 ways we can update the replicas
			* ### directly update the replicaset-definition.yml file
				replicas : 6 ( EX: previously it was 4 )
				kubectl replace -f replicaset-definition.yml
			* ### Through command line  - without modifying replicaset-definition file
				* ### kubectl scale --replicas=6 -f replicaset-definition.yml
				* ### kubectl scale --replicas=6 replicaset frontend (replicaset_name). Here type=replicaset and name=frontend
		* ## Delete replicaset / pod
			kubectl delete replicaset replicaset_name
			kubectl delete pod pod_name
		* ## selectors vs labels
			replicaset-definition.yml
			 spec:
			   replicas: 3
			   selector:
			     matchLabels:
			       tier: front-end
			   template:
			    //Define pod info
			pod-definition.yml
			   metadata:
			     name: name of the pod / replica set / replication controller
			     labels:
			       tier:  front-end
 	* ### Deployment:
 	 	* kind = Deployment
 	 	* deployment-definition file is similar to replica set.
 	 	* Maintain Deployment activities such as maintain rollout, versioning, etc
 	 	* Rollout & Revision: 
 	 		* each deployment trigger rollout which will create new deployment revision EX: revision 1
 	 		* When we want to update the image version, new deployment takes place where it triggers new rollout which will create new  	
 	 		  revision EX: revision 2
 	 	* Recreate:
 	 		* Deployment action first scal down the exsiting running instance and scale up the new instances
 	 	* RollingUpdate:
 	 		* Deployment action scale down exisitng instance one at a time and scale up the new instances.
 	 		* This is default update
 	 	* Upgrades:
 	 		* Deployment object first create replica set (ex: replicaset 1) which will create specified no of containers on it
 	 		* When next deployment happens, it creates a new replica set (ex: replicaset 2) and scale down existing instances one at a time 
 	 		  in the replica set 1 and scale up new containers in newly created replica set 2.
		* Rollback:
			* Something is wrong in the new upgrades, we should do roll back the current deployment. It scales down the containers from 
			  replica set 2 and scale up the containers from the replica set 1.
			* Command:
				kubectl rollout undo deployment_name
	* # Network:
	* # Service:
		* Helps to make communication between pods and external services.
		* Type of services:
			* NodePort - external communication 
			* ClusterIp - internal communication ( cluster )
			* LoadBalancer - Act as a load balancer.
		* Always Keep service name as a container name.
		* <img width="379" alt="image" src="https://user-images.githubusercontent.com/10528013/208247742-4f17cbd9-c128-4153-9441-e4e7ada0cf70.png">
		* <img width="650" alt="image" src="https://user-images.githubusercontent.com/10528013/208247585-f1af8965-9fa2-484b-8de0-65851119cf3b.png">
				 
	* # Commands: kubectl - this is cmd
		* kubectl cluster-info
		* kubectl get nodes
		* kubectl run 
		* kubectl create -f pod-definition.yml
		* POD deployment:
			* kubectl run pod_name --image=image
			* kubectl create -f pod-definition.yml
			* kubectl apply -f pod-definition.yml - apply the changes
			* kubectl get pods
			* kubectl descripe pod pod_name -> gives more details about pod
			* kubectl delete pod pod_name1 pod_name2
			* kubectl get pods -o wide -> gives ip address of the pod
			* kubectl logs pod_name -> pod is having only one container
			* ubectl run redis --image=redis123 --dry-run=client -o yaml > redis-definition.yaml
			* kubectl logs pod_name -c container_name -> pod is having more than 1 container name
		* Replica set deployment:
			* kubectl run re_name --image=image
			* kubectl get replicaset
			* kubectl delete replicaset replicaset_name -> delete all the pods under this replicaset
			* kubectl explain replicaset | grep VERSION
			* kubectl edit replicaset replicaset_name -> To edit replicaset definition file
			* kubect scale --repicas=2 rs rs_name
		* Deployment:
			* kubectl create -f deployment-definiton.yml
			* kubect get all -> gives details about deployment, replicaset, pod
		* Service:
			* minikube service service_name --url
	* # Minikube: - cluster set up
		* minikube start --driver=docker
		* minikube status
			 
			 
			
			
			


		






