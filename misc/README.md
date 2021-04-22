# "misc" files
This directory contains files used on the OpenShift (ocp.devenchoice.com) machine to help with installing and managing OpenShift clusters.

## bash_profile
To use the Bash Profile file, copy it to your home directory:

```
cp bash_profile ~/.bash_profile
```

If you do not want to overwrite your own bash profile, use `diff` to see what has been included.

1. The proflie starts `ssh-agent` and then includes the SSH private key for the `ocpuser`, which has been used to provision the OCP clusters.
This key will also allows you to ssh directly into cluster machines via the `core` account.
1. The profile defines the environment variable `KUBE_EDITOR` to be `vim` (instead of the default of `vi`). 
This is done primarily to enable syntax highlighting.
1. The alias `auth` is defined. This sets the `KUBECONFIG` environment variable via the `auth/kubeconfig` file in the current directory.
1. The `oc` and `kubectl` bash completions are loaded from `~/.kube/completion.bash.inc`.

In order to create the `~/.kube/completion.bash.inc` file, use the following command:

```
oc completion bash > ~/.kube/completion.bash.inc
```

For more information about `oc completion`, execute `oc completion --help`.

## vimrc
To use the VIM settings file `vimrc`, copy it to your home directory:

```
cp vimrc ~/.vimrc
```

If you do not want to overwrite your existing `.vimrc` you should manually merge the two files.

This file ensures that:
* No tabs will be added to your files
* When you press [Tab], two spaces will be added
* Syntax highlighting will be enabled
* Block shifts (left and right) will always be by 2 spaces
* Mouse actions will be enabled (for terminal programs that support this).
