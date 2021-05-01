# Usage

## One-time setup of non-root user

Before doing anything else, the init playbook should be run. This will do a few
things:

1. Set up a non-root user
2. Disable SSH access for the root user
3. Disable SSH password authentication

Create a variable `authorized_keys` in a file `authorized_keys.yml` and set its
value to a list of SSH keys that should be permitted for remote access. Then
run the following command:

```
ansible-playbook --user root -e @authorized_keys.yml -i '<host>,' init.yml
```

## Execution

1. Take a look at site.yml and decide which sets of roles are desired. Make
note of their tags.
2. Put all required variables for the roles to be executed in variables
file(s). Sensitive parameters can be put in an encrypted file with
`ansible-vault`

The command below provides an example on how the playbook can be executed. The
optional roles tagged with `private` and `backuped` will be used, and required
variables will be read from the `params.yml` and `secret_params.yml` files.

```
ansible-playbook -K --ask-vault-password -e @params.yml -e @secret_params.yml -i '<host>,' -t private,backuped site.yml
```
