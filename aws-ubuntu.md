1. Create VM
* Login to AWS console and go to EC2 </br>
* Create key-pairs or upload yours</br>
* Start EC2 VM-> Any ubuntu free tier</br>
2. Install Docker:</br>
*	Add repo referring https://docs.docker.com/install/linux/docker-ce/centos/#install-using-the-repository </br>
*	There will be selinux dependency issue: check https://github.com/geerlingguy/ansible-role-docker/issues/56 and enable extra repos for the OS( centos or rehl)</br>
*	After adding repo, docker can be installed with yum command</br>
3. Install Minikube: https://github.com/kubernetes/minikube/releases</br>
*	Command:</br>
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/	</br>
*	minikube version</br>
*	minikube start --vm-driver=none //This command will start minikube</br>
it gives error 
```
mukesh3258@minikube:~$ minikube start --vm-driver=none
========================================
kubectl could not be found on your path. kubectl is a requirement for using minikube
To install kubectl, please run the following:

curl -Lo kubectl https://storage.googleapis.com/kubernetes-release/release/v1.13.2/bin/linux/amd64/kubectl && chmod +x kubectl && sudo cp kubectl /usr/local/bin/ && rm kubectl

To disable this message, run the following:

minikube config set WantKubectlDownloadMsg false
========================================
Starting local Kubernetes v1.13.2 cluster...
Starting VM...
Getting VM IP address...
Moving files into cluster...
Downloading kubeadm v1.13.2
Downloading kubelet v1.13.2
Finished Downloading kubeadm v1.13.2
Finished Downloading kubelet v1.13.2
E0207 11:53:10.082548   12175 start.go:302] Error updating cluster:  downloading binaries: transferring kubeadm file: &{BaseAsset:{data:[] reader:0xc00000e230 Length:0 AssetName:/home/mukesh3258/.minikube/cache/v1.13.2/kubeadm TargetDir:/usr/bin TargetName:kubeadm Permissions:0641}}: error creating file at /usr/bin/kubeadm: open /usr/bin/kubeadm: permission denied
================================================================================
An error has occurred. Would you like to opt in to sending anonymized crash
information to minikube to help prevent future errors?

To disable this prompt, run: 'minikube config set WantReportErrorPrompt false'
================================================================================
Please enter your response [Y/n]: n
Bummer, perhaps next time!


minikube failed :( exiting with error code 1
```
Docker version should be checked
unsupported docker version https://github.com/kubernetes/minikube/issues/3323, https://kubernetes.io/docs/setup/cri/#docker</br>
```
[root@minik8s ~]# minikube start --vm-driver=none
Starting local Kubernetes v1.10.0 cluster...
Starting VM...
Getting VM IP address...
Moving files into cluster...
Setting up certs...
Connecting to cluster...
Setting up kubeconfig...
Starting cluster components...
Kubectl is now configured to use the cluster.
===================
WARNING: IT IS RECOMMENDED NOT TO RUN THE NONE DRIVER ON PERSONAL WORKSTATIONS
        The 'none' driver will run an insecure kubernetes apiserver as root that may leave the host vulnerable to CSRF attacks

When using the none driver, the kubectl config and credentials generated will be root owned and will appear in the root home directory.
You will need to move the files to the appropriate location and then set the correct permissions.  An example of this is below:

        sudo mv /root/.kube $HOME/.kube # this will write over any previous configuration
        sudo chown -R $USER $HOME/.kube
        sudo chgrp -R $USER $HOME/.kube

        sudo mv /root/.minikube $HOME/.minikube # this will write over any previous configuration
        sudo chown -R $USER $HOME/.minikube
        sudo chgrp -R $USER $HOME/.minikube

This can also be done automatically by setting the env var CHANGE_MINIKUBE_NONE_USER=true
Loading cached images from config file.
```
It worked in centos 7 with below docker and minikube:
```
[root@minik8s ~]# docker --version
Docker version 18.03.0-ce, build 0520e24
[root@minik8s ~]# minikube version
minikube version: v0.30.0
```
*Install kubectl as well</br>
```
$ curl -Lo kubectl https://storage.googleapis.com/kubernetes-release/release/v1.8.0/bin/linux/amd64/kubectl && chmod +x kubectl && sudo mv kubectl /usr/local/bin/
```
Adding path ref for kubectl: https://docs.oracle.com/cd/E19062-01/sun.mgmt.ctr36/819-5418/gaznb/index.html</br>
export PATH=/usr/java/<JDK Directory>/bin:$PATH</br>
source .bashrc</br>
complete doc url: https://github.com/aws-samples/aws-workshop-for-kubernetes/blob/master/03-path-application-development/301-local-development/readme.adoc</br>

