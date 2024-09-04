This project will use Ansible to provision two NFS Servers and one other server with AutoFS.

There are two playbooks:

Playbook 1: head.yml

    This first playbook will setup two NFS servers.
    Each server will have their own unique user, who's home directories will be set up as NFS exports.

    On the AutoFS server, we will create the same two users such that when they log into the server,
    their home directories will automatically map from the NFS server.

Playbook 2: cleanup.yml

    This playbook will completely undo all the actions of the first playbook, except uninstalling the autofs and nfs-utils packages. 

To get started you must have three different nodes:

    Node1: Control Host
    Node2: Client Host 1 (user 'diego' will be established on this node with NFS Shared Home Directory)
    Node3: Client Host 2 (user 'goku' will be established on thsi node with NFS Shared Home Directory)

In order for this playbook to work, you must edit the following files:

    1. In inventory_hosts file:
    
        Add your two Client Host IPs, FQDN, or Aliases under the group [client_hosts]
        
            If using aliases or FQDN, make sure they resolve in /etc/hosts/ file
        
        Add the third Control Host IP, FQDN, or Alias under the group [control_host]
        
            If using aliases or FQDN, make sure it resolves in /etc/hosts/ file
    2. In host_vars directory:
        This directory contains host variables for this project.
        Rename each file with the same IP/FQDN/Alias used int he inventory_hosts file under group [client_hosts] followed by .yml extension
            Ex:
                dev-app-la.procore.prod1.yml or 7.71.225.121.yml or dev-app-la.yml
        Rename one file for one host, and the other file for the second host.
        Take a look in each file and take note of which user (goku or diego) is associated with each host
            You will use this information in step 3.
    3. In group_vars directory:
        This directory contains group variables for this project
        Edit the all.yml file as follows:
            Without changing the names of the variables, add the corresponding IP addresses for:
                diego_ip: ip_addr
                goku_ip: ip_addr
                control_host_ip: ip_addr
    4. In ansible.cfg file:
        Without changing the variable name (private_key_file= ), specify the path to the ansible ssh key to use to run these playbooks against your servers
        private_key_file= /path/to/file
    5. Lastly install the ansible.posix collection, otherwise you won't be able to use the firewalld and mount modules.
            $ ansible-galaxy collection install ansible.posix
