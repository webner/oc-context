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
oc-context create dev
```

## Use an OpenShift context

```
oc-context dev
```

This command will:
 - Source the `env` file of the selected context
 - Add the oc client tool in the version specified in OC_VERSION to your path
 - Set KUBECONFIG to $HOME/.config/oc-context/$OC_NAME/kubeconfig
 - Set OC_CONTEXT_NAME to "OpenShift $OC_NAME "
 - If OC_USER_CLIENT_CERTIFICATE is set to `true`:
   - Recreate the client certificate if it will expire in less than 7 days
 - If OC_TOKEN_URL is set and gnome-open is installed, it will open your browser with the token url
 - Evaluate $OC_PW_FUNCTION and login to OpenShift with your $OC_USER
 - Print all exported variabled beginning with "OC_"
 - Fork your $SHELL
 




