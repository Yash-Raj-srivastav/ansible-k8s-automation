# ansible-k8s-automation
## This repository is for running multiple deployments/jobs using a generic deployment template written in jinja2 and property files, Running a single playbbok command will take care of
- Checks if all the required tools are installed in your system, if not then fails the playbook
- Checks if the cluster is already running, if not then create a kind cluster with 6 nodes(1 control plane, 5 worker nodes)
- Apply appropriate labels on the nodes defined in node-properties.yaml file
- Apply appropriate taint on the nodes defined in node-properties.yaml file
- Checks if the required namespaces already exist, if not then create the namespaces
- Runs another playbook template.yaml to convert jinja2 template into deployment manifest files inside template folder
- Runs another playbook to pick up the manifest files and create the deployments out of them in the given namespace.
- command: `ansible-playbook -e "namespace=sit2 type=deployment" ansible-practice/playbooks/deploy-kind-cluster.yaml --tags "create-deployment"`
- command: `ansible-playbook -e "namespace=uat2 type=job" ansible-practice/playbooks/deploy-kind-cluster.yaml --tags "create-job"`

## To run this manually in your local system make sure these requirements are checked
1. **docker** should be installed(if you are using windows system then also install wsl2) to check run this command in your linux distro
   - command: `docker`
2. **k8s kind** should be installed to create a multinode cluster, to check if it is installed successfully run this command
   - command: `kind`
3. **ansible** should be installed, to check if ansible is installed properly run this command
   - command: `ansible`
4. create kind cluster with the config file I provided(It totally depends on you how many nodes you want to keep in the cluster, you can edit kind-cluster.yaml)
   - command: "kind create cluster --name _name-of-your-cluster_ --config _kind-cluster/kind-cluster.yaml_ <br />
     example: `kind create cluster --name my-cluster --config kind-cluster/kind-cluster.yaml`
5. add taints and labels to your control plane and worker nodes similar to the file which have been provided in kind-cluster/node-config folder(Tolerations are already added in the pod config and properites file) or you can look at node-properties.yaml file inside vars folder
   - command: `kubectl get nodes` <br />
   ### taint: <br />
   - command: "kubeclt taint nodes _node-name key=value:taintEffect_" <br />
     example: `kubectl taint nodes my-cluster-control-plane spray=red:NoSchedule` <br />
   ### label: <br />
   - command: "kubectl label nodes _node-name key=value_" <br />
     example: `kubectl label nodes my-cluster-worker size=small`
6. create some sample namespaces like sit2, uat2 or prd in your kind cluster
7. change directory to "ansible-k8s-automation" and run ansible playbook command like this <br />
   - command: `cd ansible-k8s-automation` <br />
   ### job: <br />
   - command: `ansible-playbook -e "namespace=uat2 type=job" ansible-practice/playbooks/deploy-kind-cluster.yaml --tags "create-job` <br />
   ### deployment: <br />
   - command: `ansible-playbook -e "namespace=sit2 type=deployment" ansible-practice/playbooks/deploy-kind-cluster.yaml --tags "create-deployment"`

<!-- ## 💪 Thanks to all Contributors
This project exists thanks to all the people who contribute — [contribute](CONTRIBUTING.md).
<div align="left">
<a href="https://github.com/Yash-Raj-srivastav/devops-roadmap/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=Yash-Raj-srivastav/devops-roadmap" />
</a>
</div> -->
## Thanks to all the contributors
<a href = "https://github.com/Yash-Raj-srivastav/devops-roadmap/graphs/contributors">
  <img src = "https://contrib.rocks/image?repo=Yash-Raj-srivastav/devops-roadmap"/>
</a>
<hr>
