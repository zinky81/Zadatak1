---


---

<h1 id="zadatak1">Zadatak1</h1>
<p>The task is to run GitLab CE on Kubernetes cluster using Minikube. This is the acceptance criteria:</p>
<ol>
<li>Application must have its own namespace.</li>
<li>Application must be stateful.</li>
<li>Application must be accessible outside the cluster.</li>
<li>Application is deployed via Kubernertes manifests.</li>
</ol>
<h1 id="author">Author</h1>
<ul>
<li>Zijad Alic</li>
</ul>
<h2 id="prerequisites">Prerequisites</h2>
<p>Before we start to solve above bullets we need to install required applications.</p>
<ul>
<li>Minikube<br>
<code>curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-OS_DISTRIBUTION-amd64 &amp;&amp; chmod +x minikube &amp;&amp; sudo mv minikube /usr/local/bin/</code></li>
<li>Kubectl<br>
<code>curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl</code></li>
<li>Docker<br>
<code>sudo apt-get install docker.io -y</code></li>   
</ul>
<h2 id="lets-begin">Let’s begin</h2>
<ol>
<li>
<p>Since we need to initiate cluster, we need to create it.</p>
<p><code>minikube start</code></p>
</li>
</ol>
<pre><code>Starting local Kubernetes cluster...
Running pre-create checks...
Creating machine...
Starting local Kubernetes cluster...
</code></pre>
<p>First condition is to have unique namespace. Let’s see what we have by default.</p>
<pre><code>kubectl get namespaces
</code></pre>
<p><code>NAME          STATUS    AGE</code><br>
<code>default       Active    1d</code><br>
<code>kube-system   Active    1d</code><br>
   <code>kube-public   Active    1d</code><br>

<p>Let create a unique namespace</p>

    kubectl create namespace zijad

<p>With this we have created namespace 'zijad'.

Now let proceed with an installation of required services for Gitlab-CE. Application required are: redis and postgres.

`kubectl --namespace=zijad create -f redis-pod.json` 
 
 `kubectl --namespace=zijad create -f redis-service.json` 
 
 For Postgres we will implement Statefulset as per request.
 
 Let start with configmap:
 
 `kubectl --namespace=zijad create -f postgres-configmap.yaml`
 
 Now, let set PersistentVolume storage:
 
 `kubectl --namespace=zijad create -f postgres-storage.yaml`
 
 Let set deployment:
 
 `kubectl --namespace=zijad create -f postgres-deployment.yaml`
 
 And finally let set postgres service:
 
 `kubectl --namespace=zijad create -f postgres-service.yaml`
 
 `apiVersion: v1
kind: Service
metadata:
  name: postgres
  labels:
    app: postgres
spec:
  type: NodePort
  ports:
   - port: 5432`
  `selector:
   app: postgres`

We need to check are those services up & running with command:

`kubectl --namespace=zijad get pods`

We should get something like:


`NAME                IMAGE(S)               HOST                LABELS              STATUS`

`redis               stable/redis      10.0.0.4/           name=redis          Running`

`postgresql          stable/postgres   10.0.0.4/           name=postgresql     Running`

Let finally create gitlab pod with command:

`kubectl --server=http://yourdomain:8080 create -f gitlab-pod.json`

Now, we want http service enabled for gitlab.

`kubectl --server=http://yourdomain:8080 create -f gitlab-service-http.json`

Since it's required that service can be accessible outside the cluster, we need to use LoadBalancer with expose command.

`kubectl expose deployment gitlab-ce --type=LoadBalancer --port=8080`
 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NjI5MTA0MjMsLTE2NzMwNDkyMDgsNj
g4NDI5NzA0LC0xODk2NTU1Mzg1LC02NDMzNzU4MjIsLTM1MDQ3
MTExNSwtMTk5NzI5NDk2MSwtMTM4NjMyODk0MywxNTkyOTY3MD
k5LDY5NjQ4NjcwMSwxOTY2NTI3MTA4LC00MDI0MTA2MTIsNjcw
MzI3NTI1LDg0ODg0NjU5MywxMjc5Mzk2OTYwXX0=
-->
