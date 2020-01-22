# Connect to Terminal

In order to connect to a PKS managed Kuberntes cluster, we will need the `pks` CLI. Further, the `kubectl` CLI is needed to manage the various Kubernetes resources/objects. These CLI tools have been downloaded onto a Jumpbox and are included in a browser based shell. You may use either of these methods to use the tools.

## Jumpbox Terminal

- Using `putty` or a similar `ssh` tool, `ssh` to the Jumpbox using the credentials handed out by the instructors:

```
ssh <username>@ubuntu-254.haas-254.pez.pivotal.io
<Enter password>
```
If you have no `ssh` client available on your workstation, you may downlaod PuTTy here: https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe

## Browser Terminal

- If you are not permitted or are unable to download an `ssh` client, you may use one of a few (~10) browser based terminals available here: https://pks-shell.cfapps.io/

- Pick one of the shell instances and obtain the password from the instructors. 

# Setup kubeconfig

- Run the following command to authenticate against the PKS API server and to setup the right `kubeconfig` that grants you access to a part of the K8s cluster set up for these labs exercises.

```
pks get-kubeconfig k8s-cluster -u <username> -a api.run.haas-254.pez.pivotal.io -k -p <password>
```

- You will be accessing the K8s API server through a load balancer that presents a certificate different from the one used by the K8s API server. Run the following commands to instruct `kubectl` to trust the cert presented to it. You will typically not have to do this in your live environment.

```
kubectl config set-cluster k8s-cluster --certificate-authority=$HOME/app/cert/kube.pem --embed-certs=true
kubectl config set-cluster k8s-cluster --insecure-skip-tls-verify=1
```
- Finally, instruct `kubectl` to use the namespace allocated to you. The name of namespace is the same as your username.

```
kubectl config set-context k8s-cluster --namespace=<username>
```

- Verify you have access to your namespace with the following command:

```
kubectl get all
```
