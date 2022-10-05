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
		○ Make a connectivity between the container
		○ Scale up and scale down the container based on the load
		○ Monitoring container health & performance
		○ Above mentioned process automatically deploying and managing is known as Orchestration
		○ Tools Available:
			§ Docker swarm
			§ Kubernetes - Google
			§ MESOS - Apache
	○ Kubernetes:
		○ Supported by all cloud service providers such as Azure, AWS, 
		○ High availability
		○ Scale up & scale down
	○ Architecture:
		○ Node: (Miniors)
			§ It is a machine on which K8S installed on it.  Node may be a physical Machine / Virtual Machine.
			§ Our application runs on this
		○ Cluster:
			§ It has more than 1 node and group together
		○ Master Node:
			It is nothing but a Node on which K8S installed on it and marked as Master.






