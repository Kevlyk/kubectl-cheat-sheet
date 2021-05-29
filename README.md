How many nodes does your cluster have?
(the answer should be the kubectl command you used to get the answer)
$ kubectl get node
NAME             STATUS   ROLES    AGE   VERSION
docker-desktop   Ready    master   18h   v1.19.7

What kernel version and what container engine is each node running?
(the answer should be the kubectl command you used to get the answer)
kubectl version
Client Version: version.Info{Major:"1", Minor:"21", GitVersion:"v1.21.0", GitCommit:"cb303e613a121a29364f75cc67d3d580833a7479", GitTreeState:"clean", BuildDate:"2021-04-08T16:31:21Z", GoVersion:"go1.16.1", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"19", GitVersion:"v1.19.7", GitCommit:"1dd5338295409edcfff11505e7bb246f0d325d15", GitTreeState:"clean", BuildDate:"2021-01-13T13:15:20Z", GoVersion:"go1.15.5", Compiler:"gc", Platform:"linux/amd64"}
WARNING: version difference between client (1.21) and server (1.19) exceeds the supported minor version skew of +/-1

kubectl describe node <docker-desktop>

kubectl get nodes -o wide

List only the pods in the kube-system namespace.
(the answer should be the kubectl command you used to get the answer)
$ kubectl get pods -n kube-system
NAME                                     READY   STATUS    RESTARTS   AGE
coredns-f9fd979d6-4fj2r                  1/1     Running   0          19h
coredns-f9fd979d6-bnhz4                  1/1     Running   0          19h
etcd-docker-desktop                      1/1     Running   0          19h
kube-apiserver-docker-desktop            1/1     Running   0          19h
kube-controller-manager-docker-desktop   1/1     Running   0          19h
kube-proxy-pmbpz                         1/1     Running   0          19h
kube-scheduler-docker-desktop            1/1     Running   1          19h
storage-provisioner                      1/1     Running   0          19h
vpnkit-controller                        1/1     Running   0          19h


Explain the role of some of these pods.
etcd:store critical data
coredns: internal dns
apiserver: api server
kube-scheduler: for cron

If there are few or no pods in kube-system, why could that be?
kubernetes is not running?

On some clusters, the control plane is located outside the cluster itself, and not running as containers.                                                   

In that case, the control plane won't show up in kube-system, but you can find on host with ps aux | grep kube.

Create a deployment using kubectl create that runs the image bretfisher/clock and name it ticktock.
(the answer should be the kubectl command you used)
$ kubectl run ticktock --image bretfisher/clock
pod/ticktock created
kubectl create deployment ticktock --image=bretfisher/clock



Increase the number of pods running in that deployment to three.
(the answer should be the kubectl command you used)
kubectl scale deployment/ticktock --replicas=3

Use a selector to output only the last line of logs of each container.
(the answer should be the kubectl command you used)
kubectl logs -l run=ticktock

$ kubectl get replicaset
$ kubectl get deployment
