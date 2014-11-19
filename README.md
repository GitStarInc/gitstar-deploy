# Mac OS X Setup

```sh
brew install ansible
pip install pycurl linode-python
```

# Running ansible
Note that there are a few passwords and keys necessary to actually execute the scripts. Please contact your local administrator to get that information. There are also aliases that will eventually be factored out but remain in place for now.

```sh
ansible-playbook -i [production|stage] site.yaml -K --ask-vault-pass
```

# Ansible Vault
Some sensitive information is source controlled but encrypted to ensure some level of security. To edit files that are ansible encrypted you must have the vault password and edit the file using the `ansible-vault` command.

```sh
ansible-vault edit <filename>
```
