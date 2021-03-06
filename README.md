# helm-sudo plugin

A [helm](https://helm.sh) plugin that uses impersonating to execute helm-commands on clusters within the admin context.

## Installation

Install the plugin using the built-in plugin manager (see [releases](https://github.com/cloudogu/helm-sudo/releases)  for latest version):

```
# Installs latest commit
helm plugin install https://github.com/cloudogu/helm-sudo
# Installs deterministic version
helm plugin install  https://github.com/cloudogu/helm-sudo --version=0.0.1
``` 

---

## Usage

Its usage is pretty simple, just use "sudo" on your helm commands like so:

```
helm sudo list 
```

what the plugin does is, it adds the --kube-as-user and --kube-as-group flags with your user ($USER) and system:masters group to the given helm command. 

So the plugin executes the following: 

```
helm --kube-as-user $USER --kube-as-group system:masters list
```

Flags will just be passed along to the command you are calling. 

**CAUTION: Due to the usage of this plugin, you will execute the helm command as admin on your cluster!**

---

## Configuration

| ENV_VAR  	|   Default	|   Description	|   
|---	|---	|---	|
|HELM_SUDO_PROMPT|   	false |   If set to true you will be prompted to acknowledge the usage of the helm-command on the current context as admin	|


## Similar projects
* [cloudogu/kubectl-sudo](https://github.com/postfinance/kubectl-sudo): Same functionality as helm-sudo for kubectl
* [cloudogu/sudo-kubeconfig](https://github.com/cloudogu/sudo-kubeconfig): Create a sudo kubeconfig for your current kubernetes context.
