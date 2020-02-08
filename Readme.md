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
<p><code>Name Status Age</code><br>
<code>default Active 1m</code></p>
<p>Our condition is to have unique namespace, so let’s create json file ‘namespace.json’ and label it as ‘zijad’ .<br>
<code>{ "apiVersion": "v1", "kind": "Namespace", "metadata": { "name": "zijad", "labels": { "name": "zijad" } } }</code></p>
<p>With this we have created json file that we need to execute for our Kubernetes cluster.</p>
<p>Let’s execute json file.</p>
<p><code>kubectl create -f https://github.com/zinky81/Zadatak1/namespace.json</code></p>
Now let initiate Helm

    helm init
It's time to proceed with Gitlab CE installation

    helm install --namespace zijad --name Gitlab-CE \
    --set externalUrl=http://your-domain.com/ stable/gitlab-ce


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQwMjQxMDYxMiw2NzAzMjc1MjUsODQ4OD
Q2NTkzLDEyNzkzOTY5NjBdfQ==
-->