# oc-context
A script to login and manage different OpenShift clusters in your terminal.

## Dependencies
This scripts needs oc-select (https://github.com/webner/oc-select) and if you want to use client certificates openssl.

## Installation
```
mkdir -p $HOME/.local/bin
cd $HOME/.local/bin
wget -q https://raw.githubusercontent.com/webner/oc-context/master/oc-context
chmod +x oc-context
```

Add $HOME/.local/bin to your PATH.
```
export PATH="$PATH:$HOME/.local/bin"
```

## Usage
```
$ oc-context help

usage: oc-context <cmd>|<context>
--------------------------------------------
help              show usage information
list              list all availabe contexts
create <context>  create a new context
edit <context>    edit config
delete <context>  deletes a context
[use] <context>   use a context
create-cert       create user certificate
```

## Create a new OpenShift context
The configuration for a context is stored in a file located at $HOME/.config/oc-context/$OC_NAME/env
With the following command a new context `dev` will be created and the `env` file will be opened in your $EDITOR

```
$ oc-context create dev
```

## Import an OpenShift context
The prefered way to create new context is to first connect to the OpenShift cluster and than run the import command. With this method most of the settings will be automatically discovered.

```
$ oc login
$ oc-context import dev
```

## Use an OpenShift context

```
$ oc-context dev

  ___                 ___ _    _  __ _                _           _
 / _ \ _ __  ___ _ _ / __| |_ (_)/ _| |_   __ ___ _ _| |_ _____ _| |_
| (_) | '_ \/ -_) ' \\__ \ ' \| |  _|  _| / _/ _ \ ' \  _/ -_) \ /  _|
 \___/| .__/\___|_||_|___/_||_|_|_|  \__| \__\___/_||_\__\___/_\_\\__|
      |_|

OC_CONSOLE                 https://openshift-dev.example.org/settings/cluster
OC_REGISTRY                openshift-dev-registry.example.org
OC_TOKEN_URL               https://oauth-openshift.example.org/oauth/token/request
OC_URL                     openshift-dev.example.org:6443
OC_USER                    webner
OC_VERSION                 4.3
```

This command will:
 - Source the `env` file of the selected context
 - Add the oc client tool in the version specified in OC_VERSION to your path
 - Set KUBECONFIG to $HOME/.config/oc-context/$OC_NAME/.kubeconfig
 - Print all exported variabled beginning with "OC_"
 - Login to the cluster with client certificate or password.
 - Fork a new $SHELL


## Show current context in your shell

For ZSH add following to $HOME/.zshrc
```
export PROMPT="$OC_CONTEXT_INFO$PROMPT"
```

For Bash add following to $HOME/.bashrc
```
export PS1="$OC_CONTEXT_INFO$PS1" 
```
