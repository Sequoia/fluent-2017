## Todo

* [ ] Look through this https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

### PHASE 0: demo python app
https://github.com/janakiramm/kubernetes-101
* [X] ~~*Local (minikube)*~~
* [X] ~~*Set up GKE*~~
* [ ] Push to GKE

### PHASE I
* [X] ~~*Dockerize a micro/node app*~~
* [X] ~~*Run it*~~
* [X] ~~*Push it to docker registry*~~
* [x] Install minikube
  * [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#before-you-begin)
  * [minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)
* [X] ~~*Run minikube*~~
  * `minikube start --logtostderr`
  * Where is my config file it's supposed to create?
    * should be in `~/.kube/`
  * **The command just takes a long time**
  * `minikube status`
  * `minikube ssh`
  * `kubectl cluster-info`
  * `kubectl get` &larr; see everything you can get
  * `kubectl get cs` container statuses
  * `minikube service list`
    * **get dashboard URL**
    * **get service urls**
  * `kubectl exec -it web /bin/bash`
* [ ] Create kubernetes version
* [ ] Expose port 80
* [ ] Run the kubernetes version locally & hit 80
* [ ] Check out other ways to look at it (other UIs)
* [ ] Figure out how to add minikube/kubernetes certs to the browser

### PHASE II
* [ ] Do a version with a node app + redis server
* [ ] Env vars
* [ ] Try connecting out to mongolab
* [ ] Scale

### PHASE III
* [ ] Proxy requests
* [ ] Deploy the kubernetes version somewhere


## Why Containers
[source](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/) (good explanation of kubernetes' benefits and those of containerization generally)

* Agile application creation and deployment: Increased ease and efficiency of container image creation compared to VM image use.
* Continuous development, integration, and deployment: Provides for reliable and frequent container image build and deployment with quick and easy rollbacks (due to image immutability).
* Dev and Ops separation of concerns: Create application container images at build/release time rather than deployment time, thereby decoupling applications from infrastructure.
* Environmental consistency across development, testing, and production: Runs the same on a laptop as it does in the cloud.
* Cloud and OS distribution portability: Runs on Ubuntu, RHEL, CoreOS, on-prem, Google Container Engine, and anywhere else.
* Application-centric management: Raises the level of abstraction from running an OS on virtual hardware to run an application on an OS using logical resources.
* Loosely coupled, distributed, elastic, liberated micro-services: Applications are broken into smaller, independent pieces and can be deployed and managed dynamically – not a fat monolithic stack running on one big single-purpose machine.
* Resource isolation: Predictable application performance.
* Resource utilization: High efficiency and density.

# Kubernetes concepts

* [ ] Try quickstart: https://cloud.google.com/container-engine/docs/quickstart
* [ ] REWRITE DEMO TO USE DEPLOYMENT INSTEAD OF RC: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/
* [ ] Try out the UI to deploy: https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

# More info

* kubectl Cheat sheet https://kubernetes.io/docs/user-guide/kubectl-cheatsheet/
* Kubernetes dashboard tour: https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
* "Kubernetes Pods are mortal. They are born and when they die, they are not resurrected. ReplicationControllers in particular create and destroy Pods dynamically (e.g. when scaling up or down or when doing rolling updates)." https://kubernetes.io/docs/concepts/services-networking/service/
* **set up the bash completion!!** Lots of commands, much easier with it set up:
  * `kubectl completion --help`
* https://github.com/johanhaleby/kubetail

# GKE

https://kubernetes.io/docs/getting-started-guides/gce/#getting-started-with-your-cluster

## Set up

https://deis.com/blog/2016/first-kubernetes-cluster-gke/

* [ ] STEP THROUGH THIS PROCESS ON A NEW ACCOUNT!

1. Create or link account: https://cloud.google.com/container-engine/
2. (You'll eventually need to enter billing info to run containers but you get some free credits & be warned before you're charged)
3. Create a project https://console.cloud.google.com/kubernetes/list?project=sl-stats
  * Dashboard: https://console.cloud.google.com/home/dashboard?project=sl-stats
4. Create a "cluster"
  * **THIS SETUP WAS INADEQUATE TO RUN 2x WEB + 1x REDIS!**
  * [ ] Create node-pool with more CPUs, enough to run this properly
  * 1 cpu
  * container-vm
  * size: 1
  * Note the "zone"
5. Install `gcloud` command line tool: https://cloud.google.com/sdk/docs/quickstarts
  * initialize the tool: https://cloud.google.com/sdk/docs/quickstarts
  1. `gcloud auth list`
6. Navigate to project list
  * Sidebar menu
  * "Container Engine"
  * (pin this for easy location later)
7. Click "connect"
  * `gcloud container clusters get-credentials <cluster-name> --zone <zone-name> --project <project-name>`
  * Check new context: `kubectl get contexts`
  * See that it's current context: `kubectl config current-context`
  * `kubectl proxy` to create a local proxy to the GKE dashboard
8. Rename the context in `~/.kube/config` for convenience

## To switch from local minikube to GKE & back:

### Get available contexts

```
$ kubectl config get-contexts
CURRENT   NAME                                        CLUSTER                                     AUTHINFO                                    NAMESPACE
          minikube                                    minikube                                    minikube
*         gke_sl-stats_us-central1-a_test-cluster-1   gke_sl-stats_us-central1-a_test-cluster-1   gke_sl-stats_us-central1-a_test-cluster-1
```

### Get current context

```
$ kubectl config current-context
gke_sl-stats_us-central1-a_test-cluster-1

# To see *all* configuration values (note `current-context`):
$ kubectl config view
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: REDACTED
    server: https://35.184.227.130
  name: gke_sl-stats_us-central1-a_test-cluster-1
- cluster:
    certificate-authority: /Users/sequoia/.minikube/ca.crt
    server: https://192.168.99.100:8443
  name: minikube
contexts:
- context:
    cluster: gke_sl-stats_us-central1-a_test-cluster-1
    user: gke_sl-stats_us-central1-a_test-cluster-1
  name: gke_sl-stats_us-central1-a_test-cluster-1
- context:
    cluster: minikube
    user: minikube
  name: minikube
current-context: gke_sl-stats_us-central1-a_test-cluster-1
kind: Config
preferences: {}
users:
- name: gke_sl-stats_us-central1-a_test-cluster-1
  user:
    auth-provider:
      config:
        access-token: ya29.foo.bar
        cmd-args: config config-helper --format=json
        cmd-path: /Users/sequoia/Downloads/google-cloud-sdk/bin/gcloud
        expiry: 2017-05-30T17:51:39Z
        expiry-key: '{.credential.token_expiry}'
        token-key: '{.credential.access_token}'
      name: gcp
- name: minikube
  user:
    client-certificate: /Users/sequoia/.minikube/apiserver.crt
    client-key: /Users/sequoia/.minikube/apiserver.key
```

### Switch to another context

* When you run a kubectl command, it reads `~/.kube/config` for the `current-context` value & executes the command *in that context*.
* To change the context, you change the `current-context` configuration value to the context you want.


```
$ kubectl config set current-context gke_1
Property "current-context" set.
$ kubectl config current-context
gke_1
```

There's a convenient shorthand for changing the current context: `use-context`

```
$ kubectl config current-context
gke_1

$ kubectl config use-context minikube
Switched to context "minikube".

$ kubectl config current-context
minikube
```

### optional
1. Enable cloud-shell: https://cloud.google.com/container-engine/docs/quickstart#use_google_cloud_shell
   
   Allows you to do stuff from the cloud, great for speed but we wish to push from our local config.

# Pass through (looks hard)

but the ingress controller you need likely needs support for ExternalServices, which I think either is nearly complete, or just completed for the nginx ingress.

[5:45] 
alternatively, you could possibly use something like istio to do it

[5:46] 
you would basically do this:

sequoia [5:46 PM] 
(ty for your assistance)

chancez [5:47 PM] 
- deploy ingress
- create externalName service the points to your lambda endpoint
- configure ingress rule for host: "host123" to point to your service
- create service (loadbalancer or nodeport) for your ingress controller
- point traffic at your ingress service

[5:48] 
as of the nginx ingress 0.9.0-beta.4, they support externalName, so you can use nginx ingress for this i think (link:  https://github.com/kubernetes/ingress/blob/master/controllers/nginx/Changelog.md#09-beta4) (edited)

sequoia [5:48 PM] 
ah! Thank you!