# ansible-k8s-automation
This repository is for running multiple deployments using a single properties file and a generic deployment template which can be changed into k8s Jobs or Cron Jobs.

# To run this in your local system make sure these requirements are checked
1. docker should be installed(if you are using windows system then also install wsl2)
2. k8s kind should be installed to create a multinode cluster
3. ansible should be installed
4. create kind cluster with the config file I provided(It totally depends on you how many nodes you want to keep in the cluster)
   - command: "kind create cluster --name <name-of-your-cluster> --config <path-to-cluster-config-file>"
5. add taints and labels to your control plane and worker nodes similarly to the file which have been provided in kind-cluster/node-config folder(Tolerations are already added in the pod config and properites file)
6. create some sample namespaces like sit2, uat2 or prd
7. change directory to the foler where template.yaml is located and run ansible playbook command like this
   - command: "ansible-playbook -e namespace=<any-of-above-mentioned-namespace-or-your-own> template.yaml"
