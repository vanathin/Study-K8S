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
		* Both used to manage the POD life cycle
		* Based on replicas defined in the file, replication controller/Replica set make sure pods running always
		* Replica set - newest one. Replication controller - older one
	* ### Replication Controller / Replica set:
		* Sample file
		* <img width="764" alt="image" src="https://user-images.githubusercontent.com/10528013/201679528-0f1d378d-8d16-4fff-8ca4-9784a0dd8b1c.png">
	* ### Command
		* ## Create Pod / Replication controller / replica set
			kubectl create -f fileName of Pod / replica controller / replica set
		* ## See the created pod / Replication controller / replica set
			kubectl get pods / replicaset / replicationcontroller
		* ## Scale the pod using command
			kubectl scale --replica = 6 -f replicaset-definition.yml
			kubectl replace -f -f replicaset-definition.yml - Using replicaset-definition.ymls file change
		* ## Delete replicaset
			kubectl delete replicaset replicaset_name
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
			       
			 With the help of selector & labels replica set monitor group of pod instances ( manages the group of similar pod instances).
			 
			 
			
			
			


		






