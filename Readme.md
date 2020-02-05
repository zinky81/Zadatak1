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
<h2 id="switch-to-another-file">Switch to another file</h2>
<p>All your files and folders are presented as a tree in the file explorer. You can switch from one to another by clicking a file in the tree.</p>

