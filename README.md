# cloud-projects
How to better use IBMCloud together with Google Cloud Plattform.

How to better switch betwene accounts in IBM Cloud.

How to better update the accounts token every time you connect to the IBMCloud

1.

Concider using zsh 

```
sudo apt-get install zsh zsh-completions
```

Configure oh-my-zsh
[GitHub](https://github.com/robbyrussell/oh-my-zsh "Title").

Change Themes to "bira" by adding this in the .zshrc file:
```
ZSH_THEME="bira"
```

Using the bash aliases in zsh:
In .zshrc file
```
source $HOME/.bash_aliases
source /etc/zsh_command_not_found
```
Consider using the kube-ps1

https://github.com/jonmosco/kube-ps1

in .zshrc ...
```
source $HOME/bin/kube-ps1.sh
PROMPT='$(kube_ps1)'$PROMPT
```

Consider using the "merge kubeconfig" 

https://gist.github.com/dcberg/7e03a8363b30663ad20aeebf4a0f9663

in .zshrc ...
```
export KUBECONFIG=$(~/bin/iks-merged-config.sh)
```

2.

[IBM Cloud](https://cloud.ibm.com "Title"). Download the api-key for every account.

Save them in a safe place:
```
$HOME/.ssh
```
manage - access (IAM) - IBM Cloud API Key

Create "classic infrastructure API Key"

Refere this to a singlelayer key (add the key in the file)

-> export TF_VAR_ibm_sl_api_key="$(cat ~/.ssh/$ENV-ibm-sl)"'

Place the username in a separate file

-> export TF_VAR_ibm_sl_username="$(cat ~/.ssh/$ENV-ibm-sl-username)"

The username is fount in "details" for the "classic infrastructure API Key"

Create an IBM Cloud API Key

Place the API Key in a single file

-> export TF_VAR_ibm_bx_api_key="$(cat ~/.ssh/$ENV-ibm)" 


3.

Download the ibm-connect file from this GitHub

```
#!/bin/bash
ENV=${1:-rtd}
case "$ENV" in
# edit the correct project name
"rtd" | "dev" | "stage" | "prod")
    echo "Setting IMB terraform & cli to: $ENV"
# here we set the correct api-key for each project 
    export TF_VAR_ibm_bx_api_key="$(cat ~/.ssh/$ENV-ibm)"
    export TF_VAR_ibm_sl_username="$(cat ~/.ssh/$ENV-ibm-sl-username)"
    export TF_VAR_ibm_sl_api_key="$(cat ~/.ssh/$ENV-ibm-sl)"
# we do not want any interupts about version number
    ibmcloud config --check-version=false
# log in  using the api-key
    ibmcloud login -g Default -r eu-de --apikey $TF_VAR_ibm_bx_api_key
#    export KUBECONFIG=/home/steinar/.bluemix/plugins/container-service/clusters/$ENV/kube-config-osl01-$ENV.yml
#    instead of this export KUBECONFIG it's better to set the kubeconfig for all config files.
#    use  this instead:  https://gist.github.com/dcberg/7e03a8363b30663ad20aeebf4a0f9663
#    Next line sets and downloads the Kubernetes config in IBMCloud....
    ibmcloud cs cluster-config $ENV
#   When using zsh with ohmyzsh it's nice to have the correct project in the prompt.
#   https://github.com/ahmetb/kubectx using the kubectx
    kubectx $ENV
If you need to log into the softlayer uncomment next line
#    ibmcloud sl init -u $TF_VAR_ibm_sl_username -p $TF_VAR_ibm_sl_api_key
    ;;
*)
    echo "Acceptable values are rtd, dev, stage, and prod"
    ;;
esac 

```

Edit the script to your needs. See comments in script.


**Thanks to**

Espen Blikra

https://github.com/ahmetb

https://gist.github.com/dcberg

https://gist.github.com/robbyrussell

https://gist.github.com/jonmosco


