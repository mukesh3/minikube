1. Create VM
* Login to AWS console and go to EC2 </br>
* Create key-pairs or upload yours</br>
* Start EC2 VM-> Any ubuntu free tier</br>
2. Install Docker:</br>
*	Add repo referring https://docs.docker.com/install/linux/docker-ce/centos/#install-using-the-repository </br>
*	There will be selinux dependency issue: check https://github.com/geerlingguy/ansible-role-docker/issues/56 and enable extra repos for the OS( centos or rehl)</br>
*	After adding repo, docker can be installed with yum command</br>
3. Install Minikube:</br>
*	Command:</br>
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/	</br>
*	minikube version</br>
*	minikube start --vm-driver=none //This command will start minikube</br>
*	install kubectl as well</br>

Adding path ref: https://docs.oracle.com/cd/E19062-01/sun.mgmt.ctr36/819-5418/gaznb/index.html</br>
export PATH=/usr/java/<JDK Directory>/bin:$PATH</br>
source .bashrc</br>
complete doc url: https://github.com/aws-samples/aws-workshop-for-kubernetes/blob/master/03-path-application-development/301-local-development/readme.adoc</br>
unsupported docker version https://github.com/kubernetes/minikube/issues/3323, https://kubernetes.io/docs/setup/cri/#docker</br>
