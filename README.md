Consensus: Amdin Users
======================

Creates admin users. Adds an 'ansible' role that provides password-less sudo access, suitable for running Ansible.

Requirements
------------

None.

Role Variables
--------------

You'll need to provide a list of admin users under the variable `admin_users`. You probably want to put this somewhere global, so that these users are consistently created on all servers. However, you're free to set them on a host-by-host basis as well. `name` and `ssh_pub_key` are the only required elements.

    admin_users:
      - name: ergonlogic                 # Required.
        comment: Christopher Gervais     # Optional, defaults to ''.
        shell: /bin/bash                 # Optional, defaults to '/bin/bash'.
        groups: 'sudo,adm'               # Optional, defaults to 'sudo,adm,ansible'.
        password: "$6$r4r..."            # Optional, defaults to '*', i.e., no password.
        ssh_pub_keys:                    # Required.
          - "ssh-rsa AAAAB3..."


Dependencies
------------

None.

Example Playbook
----------------

Include as you would any other role. You can optionally add host-specific users like so:

    - hosts: servers
      vars:
        local_admin_users:
          - name: joe
            ssh_pub_keys:
              - "ssh-rsa AAAAB3..."
        admin_users: "{{ admin_users + local_admin_users }}"
      roles:
         - consensus.admin_users

License
-------

GNU AGPLv3

Author Information
------------------

Originally written by [Christopher Gervais](https://consensus.enterprises/team/christopher/) in 2016. Updated with contributions from [Dan Friedman](https://consensus.enterprises/team/dan/) and the folks at [Consensus Enterprises](https://consensus.enterprises). To contact us, please use our [Web contact form](https://consensus.enterprises/#contact).
