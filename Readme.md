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
<li>Minicube<br>
<code>curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-OS_DISTRIBUTION-amd64 &amp;&amp; chmod +x minikube &amp;&amp; sudo mv minikube /usr/local/bin/</code></li>
<li>Kubectl<br>
<code>curl -Lo https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/OS DISTRIBUTION/amd64/kubectl</code></li>
</ul>
<h2 id="lets-begin">Let’s begin</h2>
<ol>
<li>
<p>Since we need to initiate cluster, we need to create it.</p>
<p><code>minicube start</code></p>
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

 `kubectl --namespace=zijad --server=http://yourdomain:8080 create -f redis-pod.json` 
`kubectl --namespace=zijad --server=http://yourdomain:8080 create -f redis-service.json` 
`kubectl --namespace=zijad --server=http://yourdomain:8080 create -f postgres-pod.json `
`kubectl --namespace=zijad --server=http://yourdomain:8080 create -f postgres-service.json`

Since it's required that service can be accessible outside the cluster, we need to use LoadBalancing or 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNTk4ODIzNjIsLTM1MDQ3MTExNSwtMT
k5NzI5NDk2MSwtMTM4NjMyODk0MywxNTkyOTY3MDk5LDY5NjQ4
NjcwMSwxOTY2NTI3MTA4LC00MDI0MTA2MTIsNjcwMzI3NTI1LD
g0ODg0NjU5MywxMjc5Mzk2OTYwXX0=
-->