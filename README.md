# cloud-projects
How to better use IBMCloud together with Google Cloud Plattform.

How to better switch betwene accounts in IBM Cloud.

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

2.
Go to you IBMCloud account

Picture


Download the api-key
for every account.
Save them in a safe place:
$HOME/.ssh


Third

Download the ibm-connect file here

Edit the script to your needs. se comments in script






Thanks to

Espen Blikra
https://github.com/ahmetb
https://gist.github.com/dcberg
https://gist.github.com/robbyrussell
https://gist.github.com/jonmosco


