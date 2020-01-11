# k8s-resources

Useful Links:
	• https://github.com/keikoproj/keiko/blob/master/presentations/Keiko.pdf
	• https://blog.jayway.com/2018/10/22/understanding-istio-ingress-gateway-in-kubernetes/
	• https://github.com/kubernetes/sample-controller/blob/master/docs/controller-client-go.md
	• https://link.medium.com/6ofbxXeAyW Kubernetes controller in depth
	• https://engineering.bitnami.com/articles/a-deep-dive-into-kubernetes-controllers.html
	• https://kubedex.com/google-gke-vs-microsoft-aks-vs-amazon-eks/
	• https://kubernetes.io/docs/reference/setup-tools/kubeadm/implementation-details/
	• https://stackoverflow.com/questions/48755931/tenant-isolation-with-kubernetes-on-networking-level
	• Managing a Multi-Tenanted Kubernetes Cluster in Production by Josh Bowen, Apigee
	• https://groups.google.com/forum/m/#!forum/kubernetes-wg-multitenancy
	• https://docs.microsoft.com/en-us/azure/aks/ingress
	• https://medium.com/@evnsio/managing-my-home-with-kubernetes-traefik-and-raspberry-pis-d0330effea9a
	• https://blog.giantswarm.io/deep-dive-into-kubernetes-networking-in-azure/
	• https://docs.projectcalico.org/v3.0/reference/public-cloud/azure
	• https://kubernetes.io/blog/2015/06/the-distributed-system-toolkit-patterns/
	• https://abhishek-tiwari.com/a-sidecar-for-your-service-mesh/
	
	
	• Life of a Packet [I] - Michael Rubin, Google
	
	
	• Kubernetes - Carson
	
	
	• https://medium.com/google-cloud/experimenting-with-cross-cloud-kubernetes-cluster-federation-dfa99f913d54
	• https://container-solutions.com/kubernetes-deployment-strategies/
	• https://console.bluemix.net/docs/containers/cs_loadbalancer.html#loadbalancer
	• https://console.bluemix.net/docs/containers/cs_ingress.html#ingress
	• https://medium.com/ibm-cloud/deploy-applications-across-multiple-clusters-using-ibm-cloud-private-27dca31c5db2
	• https://thenewstack.io/configuring-kubernetes-cluster-federation-to-create-a-global-deployment/
	• https://github.com/containerd/cri/blob/master/contrib/ansible/README.md (kubernetes and containerd using ansible scripts)
	• https://kubernetes.io/docs/setup/scratch/
	• https://github.com/kubernetes/kubeadm/issues/17 build a docker kubernetes image
	• https://medium.com/@lizrice/kubernetes-in-vagrant-with-kubeadm-21979ded6c63
	• http://michele.sciabarra.com/2018/02/12/devops/Kubernetes-with-KubeAdm-Ansible-Vagrant/
	• https://medium.com/@jimmysongio/setting-up-a-kubernetes-cluster-with-vagrant-and-virtualbox-3bb854017b60
	• https://docs.projectcalico.org/v2.3/getting-started/kubernetes/installation/vagrant/
	• https://docs.platform9.com/support/disabling-swap-kubernetes-node/
	• https://medium.com/@AnushkaSandaru1/how-to-change-expired-certificates-in-kubernetes-cluster-5d3feb9d9838
	• https://github.com/kubernetes/kubeadm/issues/338 resetting master ip address
	• http://alesnosek.com/blog/2017/02/14/accessing-kubernetes-pods-from-outside-of-the-cluster/
	• https://stackoverflow.com/questions/47057176/how-to-access-kubernetes-service-externally-on-bare-metal-install
	• The ins and outs of networking in Google Container Engine and Kubernetes  (Google Cloud Next '17)
	
	
	• https://thenewstack.io/tutorial-run-multi-node-kubernetes-cluster-digitalocean/
	• https://www.ibm.com/blogs/bluemix/2018/08/single-service-mesh-with-istio-against-multiple-hybrid-clusters/
	• https://github.com/crossplaneio/crossplane
	• https://www.devopstoolkitseries.com/
	• https://github.com/kubernetes/kubernetes/issues/27081#issuecomment-238078103

Notes:
	• IP connectivity between nodes
	• IP per Pod on the virtual network
	• Rich network policy contructs for isolation (labels, namespaces, etc).  This allows for decoupling isolation from network topology
	• By default, every pod can communicate directly with every other pod
	• No port mapping schemes required
	• Each pod is given a virtual interface connected to an internal
	• Each node has a running network stack
	• Kube-proxy runs in the OS to control iptables
	• Pod network is not seen on the physical network
	• Ingresses are entry points into the kubernetes network
	• Most ingresses are layer 7 load balancers (i.e. http/https)
	• Ingress sits on the physical network and talks to the endpoints directly and not through the service.
	• Cluster ip is used to talk within the cluster like microservice to microservice
	• Container networking means never having to ask "what port is it on" because every service has its own ip address in the container network
	• How does the container network find ip address and that is through a dns.
	• https://github.com/ramitsurana/awesome-kubernetes
	• https://docs.microsoft.com/en-us/azure/aks/http-application-routing
	• Type 3 Master configuration:
		○ All 3 have kube-apiserver, kube-scheduler, and kube-controller-manager
		○ For kube-scheduler and kube-controller-manager only one instance of each of these can be active at a time across the 3 masters.
	• Kube-apiserver, kube-scheduler, and kube-controller-manager are usually always ran on docker containers on the master with a instance of kubelet to manage traffic to them
	• All nodes have kubelet and kube-proxy (or substitute)
	• LoadBalancer services do not support TLS termination. If your app requires TLS termination, you can expose your app by using Ingress, or configure your app to manage the TLS termination.
	• Kubernetes limits
		○ No more than 5000 nodes
		○ No more than 150000 total pods
		○ No more than 300000 total containers
		○ No more than 100 pods per node
	• Role and RoleBinding apply to a namespace.  ClusterRole and ClusterRoleBinding apply across the entire cluster

Kubernetes certificates:
	• Multiple Api Servers must be fronted by a load balancer
	• Each master has its own certificate
	• Load balancer's dns name and IP address should be part of the certificate' Subject Alternative Name (SAN) field or clients will complain with NET-ERR_CERT_COMMON_NAME_INVALID
	• View kube apiserver certificate expiration: 
	 openssl x509 -in /etc/kubernetes/pki/apiserver.crt -noout -text |grep ' Not '
	• https://stackoverflow.com/questions/52345939/how-to-update-k8s-certificates-safely-and-completely
	• https://www.openssl.org/
	• https://kubernetes.io/docs/concepts/cluster-administration/certificates/
	

Kubeadm:
	• https://kubernetes.io/docs/setup/independent/high-availability/
	• https://stackoverflow.com/questions/48930047/change-kubeadm-init-ip-address. Multi-cloud setup
	• https://blog.inkubate.io/install-and-configure-a-multi-master-kubernetes-cluster-with-kubeadm/
	• http://cloudgeekz.com/1293/kube-dev-environment-modification.html
	• https://www.ianlewis.org/en/how-kubeadm-initializes-your-kubernetes-master
	• https://softeng.oicr.on.ca/george_mihaiescu/2018/03/21/Quick-Kubernetes-installation/
	• https://medium.com/@wso2tech/multi-node-kubernetes-cluster-with-vagrant-virtualbox-and-kubeadm-9d3eaac28b98

Vagrant:
	• https://github.com/coolsvap/kubeadm-vagrant
	• https://github.com/coolsvap/kubeadm-vagrant/blob/master/Ubuntu/Vagrantfile
	• https://github.com/ecomm-integration-ballerina/kubernetes-cluster
	• https://github.com/rootsongjc/kubernetes-vagrant-centos-cluster

Raspberry Pi:
	• https://downey.io/blog/how-to-build-raspberry-pi-kubernetes-cluster/

Test Environments:
	• https://www.linkedin.com/pulse/how-kubernetes-yourself-kubeadm-ansible-vagrant-michele-sciabarr%C3%A0
	
Kubernetes commands:
	• Get status
		○ Kubectl --namespace=kube-decon get deployment,pods,service,ingress
	• Get cluster config
		○ kubectl config view
	• To restart api server: systemctl restart kube-apiserver
	• Remove any kubectl port-forward processes that may still be running:
	
	$ killall kubectl
	• Get secret value
		○ kubectl get secret jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode
		○ printf $(kubectl get secret jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode);echo
	• kubectl patch svc <my_service> -p '{"spec": {"ports": [{"port": 443,"targetPort": 443,"name": "https"},{"port": 80,"targetPort": 80,"name": "http"}],"type": "LoadBalancer"}}'
	• Decrypt certificate-authority-data key from ~/.kube/config for the cluster
		○ echo LSuperLongBase64EncodedString== | base64 -D > ca.crt
	• kubectl exec -it platformdemoapp-cp-119-7cdfc649bc-sq2l9 -n platform-demo -- /bin/sh
	• kubectl exec -it hellodemo-6889b97ff-g4cf7 -c hellodemo -- curl http://helloworldservice:9095/helloworld/
	• Determine elected leader (master) of a high availability cluster:  kubectl describe endpoints kube-scheduler -n kube-system

Kubernetes security / roles (rbac):
	• https://gravitational.com/blog/teleport-release-3/
	• https://docs.bitnami.com/kubernetes/how-to/configure-rbac-in-your-kubernetes-cluster/

Kubernetes Operators:
	• https://banzaicloud.com/blog/operator-sdk/
	• https://docs.okd.io/latest/operators/osdk-getting-started.html
	
Kubernetes Dashboard:
	• https://github.com/kubernetes/dashboard
	• https://github.com/kubernetes/dashboard/wiki/Accessing-Dashboard---1.7.X-and-above
	• https://github.com/kubernetes/dashboard/wiki/Access-control
	• https://github.com/kubernetes/dashboard/wiki/Creating-sample-user
	• https://stackoverflow.com/questions/46664104/how-to-sign-in-kubernetes-dashboard
	• https://thenewstack.io/single-sign-on-for-kubernetes-dashboard-experience/
	• Dev cluster token (user: cluster-sa)
		eyJhbGciOiJSUzI1NiIsImtpZCI6IiJ9.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6ImNsdXN0ZXItc2EtdG9rZW4teDdkdnEiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC5uYW1lIjoiY2x1c3Rlci1zYSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50LnVpZCI6ImZkOGM1NmY1LWM4MWYtMTFlOC1iZGRmLTAwMTU1ZGNkZGIwNiIsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDpkZWZhdWx0OmNsdXN0ZXItc2EifQ.ndAMAFfOs8XUtqrZ25HZUEpzPvMn2iR6WrgX11oUZvuuWuOgv5igQ2xKRbgaS4HNENdjXxY5C4AG9TrIevaO_iXVGqWB-RVhTaVUJ4pQa4SeGJuH--lttoD7EajNMFjD_EOaDEcyzCUodysKzUgjqeH1Qe5ZOWoprGkcY31FwtktDlxIdliGRDbFS7GTOI9JgZ7CMgZuzupD_FhpUmGJm3mzYCF8SKcFqziOUuZb2ovQcODFLToCIxWt3QJsbLapPPgXsx35xA70mLRGtHNMGloEOiMlhl1hDdviYu_P0QmK-wCxAIt2136iPms6Z7xT2Sy15DeX8Fd0ewBEhPvK2w

GKE:
	• https://cloud.google.com/solutions/prep-kubernetes-engine-for-prod?utm_source=free-trial-2&utm_medium=email&utm_campaign=2018-FTON-Experiment-Engagement-GKE3-en&utm_content=ft-en
	• https://cloud.google.com/solutions/prep-kubernetes-engine-for-prod
	• https://medium.com/uptime-99/making-sense-of-kubernetes-rbac-and-iam-roles-on-gke-914131b01922
	• https://medium.com/google-cloud/kubernetes-engine-kubectl-config-b6270d2b656c
	• https://medium.com/google-cloud/bash-hacks-gcloud-kubectl-jq-etc-c2ff351d9c3b

Jenkins CI/CD:
	• https://github.com/boxboat/jenkins-demo
	• https://cloud.google.com/blog/products/gcp/introducing-kaniko-build-container-images-in-kubernetes-and-google-container-builder-even-without-root-access
	• https://github.com/EamonKeane/jenkins-blue
	• https://medium.com/@vashgaurav/scaling-jenkins-with-kubernetes-4a14e6ac8f99
	• https://stackoverflow.com/questions/52897692/k8s-helm-jenkins-with-nginx-ingress
	• https://cloud.google.com/solutions/using-jenkins-for-distributed-builds-on-compute-engine
	• https://clearpoint.digital/blog/bootstrapping-jenkins-in-a-kubernetes-cluster/
	• https://kumorilabs.com/blog/k8s-6-integrating-jenkins-kubernetes/
	• https://github.com/chick-fil-a/gitops
	• https://betsol.com/2018/11/devops-using-jenkins-docker-and-kubernetes/
	• https://jenkins.io/blog/2018/09/14/kubernetes-and-secret-agents/
	• https://illya-chekrygin.com/2017/08/26/configuring-certificates-for-jenkins-kubernetes-plugin-0-12/
	• https://stackoverflow.com/questions/52522495/how-to-configure-jenkins-master-and-dynamic-agents-in-different-clouds-with-kub
	• Continuous Delivery Best Practices with Jenkins and GKE (Cloud Next '18)
	
	
	• https://github.com/jenkinsci/kubernetes-plugin/blob/master/src/main/kubernetes/service-account.yml
	• https://devops.stackexchange.com/questions/4695/jenkins-pipeline-kubernetes-agent-shared-volumes
	• https://medium.com/containerum/how-to-setup-ci-cd-workflow-for-node-js-apps-with-jenkins-and-kubernetes-360fd0499556
	• https://container-solutions.com/tagging-docker-images-the-right-way/
	• https://imti.co/gitlabci-golang-microservices/
	• https://gist.github.com/satyadeepk/b0146a0ccefc87fc41a86ea7250ec23e authenicate with gcloud using certificate
	• https://stackoverflow.com/questions/45035664/authenticate-to-google-container-service-with-script-non-interactive-gcloud-aut
	• https://github.com/wernight/docker-kubectl
Misc

	• The seven Open Systems Interconnection layers are:
		○ Layer 7: The application layer. ...
		○ Layer 6: The presentation layer. ...
		○ Layer 5: The session layer. ...
		○ Layer 4: The transport layer. ...
		○ Layer 3: The network layer. ...
		○ Layer 2: The data-link layer. ...
		○ Layer 1: The physical layer.
	• Workload Types
	Kubernetes divides workloads into different types. The most popular types supported by Kubernetes are:
		○ Deployments
Deployments are best used for stateless applications (i.e., when you don’t have to maintain the workload’s state). Pods managed by deployment workloads are treated as independent and disposable. If a pod encounters disruption, Kubernetes removes it and then recreates it. An example application would be an Nginx web server.
		○ StatefulSets
StatefulSets, in contrast to deployments, are best used when your application needs to maintain its identity and store data. An application would be something like Zookeeper—an application that requires a database for storage.
		○ DaemonSets
Daemonsets ensures that every node in the cluster runs a copy of pod. For use cases where you’re collecting logs or monitoring node performance, this daemon-like workload works best.
		○ Jobs
Jobs launch one or more pods and ensure that a specified number of them successfully terminate. Jobs are best used to run a finite task to completion as opposed to managing an ongoing desired application state.
		○ CronJobs
CronJobs are similar to jobs. CronJobs, however, runs to completion on a cron-based schedule.
	• Service Types
	There are several types of services available in Rancher. The descriptions below are sourced from the Kubernetes Documentation.
		○ ClusterIP
Exposes the service on a cluster-internal IP. Choosing this value makes the service only reachable from within the cluster. This is the default ServiceType.
		○ NodePort
Exposes the service on each Node’s IP at a static port (the NodePort). A ClusterIP service, to which the NodePort service will route, is automatically created. You’ll be able to contact the NodePort service, from outside the cluster, by requesting <NodeIP>:<NodePort>.
		○ LoadBalancer
Exposes the service externally using a cloud provider’s load balancer. NodePort and ClusterIP services, to which the external load balancer will route, are automatically created.
	
	
		
Deploying:
	• https://github.com/mcwienczek/coreos-kubernetes/blob/master/Documentation/kubernetes-on-vagrant.md
	• https://www.digitalocean.com/community/tutorials/how-to-create-a-kubernetes-1-10-cluster-using-kubeadm-on-ubuntu-16-04
	• https://www.altoros.com/blog/a-multitude-of-kubernetes-deployment-tools-kubespray-kops-and-kubeadm/
	• https://github.com/salt-formulas/salt-formula-kubernetes
	• https://salt-formulas.readthedocs.io/en/latest/_files/formulas/kubernetes/README.html
	• https://rook.io/docs/rook/master/development-environment.html
	• https://www.linode.com/docs/applications/containers/deploy-minio-on-kubernetes-using-kubespray-and-ansible/
	• https://blog.kubernauts.io/hybrid-kubernetes-with-tk8-and-rancher-2a6ad52f2937
	• https://joshrendek.com/2018/04/kubernetes-on-bare-metal/
	• https://crondev.com/kubernetes-installation-kubeadm/
	• https://docs.kublr.com/quickstart/onpremise/
	• https://www.mirantis.com/blog/how-install-kubernetes-kubeadm/
	• https://www.digitalocean.com/community/tutorials/how-to-create-a-kubernetes-1-11-cluster-using-kubeadm-on-ubuntu-18-04
	• https://wiki.onap.org/display/DW/Deploying+Kubernetes+Cluster+with+kubeadm
	• https://icicimov.github.io/blog/kubernetes/Kubernetes-cluster-step-by-step-Part2/
	• https://gravitational.com/blog/kubernetes-flannel-dashboard-bomb/

Tools:
	• https://github.com/txn2/kubefwd
	
Kubeadm:
	• Deployment steps
		○ Standup machines using Ubuntu 16.04 +
		○ Verify the MAC address and product_uuid are unique for every node
			§ You can get the MAC address of the network interfaces using the command ip link or ifconfig -a
			§ The product_uuid can be checked by using the command sudo cat /sys/class/dmi/id/product_uuid
		○ Check the required ports
			Master node(s)
			Protocol	Direction	Port Range	Purpose	Used By
			TCP	Inbound	6443*	Kubernetes API server	All
			TCP	Inbound	2379-2380	etcd server client API	kube-apiserver, etcd
			TCP	Inbound	10250	Kubelet API	Self, Control plane
			TCP	Inbound	10251	kube-scheduler	Self
			TCP	Inbound	10252	kube-controller-manager	Self
			Worker node(s)
			Protocol	Direction	Port Range	Purpose	Used By
			TCP	Inbound	10250	Kubelet API	Self, Control plane
			TCP	Inbound	30000-32767	NodePort Services**	All
			** Default port range for NodePort Services.
			Any port numbers marked with * are overridable, so you will need to ensure any custom ports you provide are also open.
			Although etcd ports are included in master nodes, you can also host your own etcd cluster externally or on custom ports.
			The pod network plugin you use (see below) may also require certain ports to be open. Since this differs with each pod network plugin, please see the documentation for the plugins about what port(s) those need.
			§ Linux command for finding out what ports are listening:
				□ sudo netstat -ntlp | grep LISTEN
				□ sudo netstat -tulpn or sudo netstat -tulpn | grep LISTEN
				□ sudo ufw status
			§ Open a range of ports:
				□ sudo ufw allow 1701
				□ ufw allow 11200:11299/tcp ufw allow 11200:11299/udp
			
			§  sudo ufw allow 10250:10252/tcp
			§  sudo ufw allow 2379:2380/tcp
			§ sudo ufw allow 6443
			§ sudo ufw allow 30000:32767/tcp
			
			
			
		○ Execute the following on all machines. (make sure to execute as root:  sudo -I )
			§ apt-get update
apt-get install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
add-apt-repository "deb https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") $(lsb_release -cs) stable"
apt-get update && apt-get install -y docker-ce=$(apt-cache madison docker-ce | grep 17.03 | head -1 | awk '{print $3}')
				□ Or
				apt-get update
apt-get install -y docker.io
			§ apt-get update && apt-get install -y apt-transport-https curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
EOF
apt-get update
apt-get install -y kubelet kubeadm kubectl
apt-mark hold kubelet kubeadm kubectl
		○ If kubeadm already installed the use the following to update
			§ apt-get update && apt-get upgrade
		○ Turn off swap
			§ swapoff -a
			§ vi /etc/fstab aand comment out swap line
		○ sudo kubeadm init --pod-network-cidr=192.168.0.0/16 --apiserver-advertise-address=142.136.205.28 --kubernetes-version 1.12.0-rc.1
		○ sudo systemctl enable docker.service
		○ https://docs.projectcalico.org/v2.6/getting-started/kubernetes/

mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config


kubeadm join 142.136.205.28:6443 --token 9oiw16.hr2ltg348zy0dimu --discovery-token-ca-cert-hash sha256:f76fc5dfd0fdf983be0a67cda2c229d26ef53a3fdef50f2e3d48bb948d152670

Setup kubectl on remote machine:
	• mkdir -p $HOME/.kube
	• scp root@142.136.205.28:/etc/kubernetes/admin.conf $HOME/.kube/config
	• sudo chown $(id -u):$(id -g) $HOME/.kube/config
Ingress Controllers:
	• https://medium.com/@carlosedp/multiple-traefik-ingresses-with-letsencrypt-https-certificates-on-kubernetes-b590550280cf

Debugging:
	• https://itnext.io/debugging-asp-net-core-in-kubernetes-from-vscode-294a728031e6
	• https://radu-matei.com/blog/state-of-debugging-microservices-on-k8s/
	• https://iboware.com/development/2018/10/12/remote-debugging-asp-net-core-applications-on-kubernetes/
	• https://developers.redhat.com/blog/2018/06/13/remotely-debug-asp-net-core-container-pod-on-openshift-with-visual-studio/
	
Tools:
	• https://github.com/ahmetb/kubectx

	• Extending (operators, custom controllers):
		○ Programming Kubernetes with the Go SDK [I] - Aaron Schlesinger, Deis
		
		

Deploy service using yaml files:
	• Create deployment
		apiVersion: extensions/v1beta1
		kind: Deployment
		metadata:
			name: GoService
			labels:
			app: GoService
		spec:
			replicas: 3
			strategy:
				type: RollingUpdate
					rollingUpdate:
					maxUnavailable: 50%
					maxSurge: 1
			template:
			metadata:
			labels:
			app: GoService
			spec:
			containers:
			- name: GoService
			image: docker.io/shannoncarver/test:GoService
			imagePullPolicy: Always
			ports:
			- containerPort: 8000
			livenessProbe:
			httpGet:
			path: /healthz
			port: 8000
			readinessProbe:
			httpGet:
			path: /readyz
			port: 8000
			resources:
			limits:
			cpu: 10m
			memory: 30Mi
			requests:
			cpu: 10m
			memory: 30Mi
			terminationGracePeriodSeconds: 30
			
		kubectl create -f deployment.yaml
		
		kubectl get deployments
		
		kubectl describe deployment GoService
		
	• Create Service
		
