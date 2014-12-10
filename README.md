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

# Adding a new application
For now we can add new applications to the `app_servers.yml` file. Just add a new dictionary with the following options.

```
role:     gitstar_create_app          - this indicates that we want to create an application
app_name: <name>                      - the name of the application. It will have a dns entry at <name>.gitstar.com
app_port: <port>                      - the port that the application is running on. Can be anything (80/8080/3000/etc).
user:     <username>                  - username of owner of git repo we are pulling the application from
repo:     <repository>                - repository that's hosting the node application
mongo:    <true|false>                - whether or not we'll have a linked mongo container for use by the application
version:  <sha1|tag|branch|HEAD|etc>  - the revision we want to deploy from the git repository
```

# Deleting an application
Similar to process for creating application, but fewer required arguments.
```
role:       gitstar_delete_app  - tells ansible to run delete role
app_name:   <name>              - name of originally deployed application
```

# Mongo
If an application requires mongodb, a mongo container will be spun up in addition to the node container. It will expose a hostname 'mongo' to the node container with mongo running at port 27017.

# Ansible Vault
Some sensitive information is source controlled but encrypted to ensure some level of security. To edit files that are ansible encrypted you must have the vault password and edit the file using the `ansible-vault` command.

```sh
ansible-vault edit <filename>
```

# Extras
I recommend installing this [vim plugin](https://github.com/chase/vim-ansible-yaml) to help make sure syntax is correct.

# TODO
- Look into ambassador pattern for linking from coreos
- ...
