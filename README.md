# Usage

## Preparation

1. Make note of which optional roles should be executed (look at the role tags
   in site.yml).
2. Put all required variables for the roles to be executed in variables file(s).
   Sensitive parameters can be put in an encrypted file with `ansible-vault`
3. Make sure the current user has SSH access to the root user on the target host.
4. Run the command below.

## Execution

The command below provides an example on how the playbook can be executed. The
optional roles tagged with `private` and `backuped` will be used, and required
variables will be read from the `params.yml` and `secret_params.yml` files.

```
ansible-playbook --ask-vault-password --user root -e @params.yml -e @secret_params.yml -i '<host>,' -t private,backuped site.yml
```
