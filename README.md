This project will use Ansible to provision two NFS Servers and one other server with AutoFS.

There are two playbooks:

Playbook 1: head.yml

    This first playbook will setup two NFS servers.
    Each server will have their own unique user, who's home directories will be set up as NFS exports.

    On the AutoFS server, we will create the same two users such that when they log into the server,
    their home directories will automatically map from the NFS server.

Playbook 2: cleanup.yml

    This playbook will completely undo all the actions of the first playbook, except uninstalling the autofs and nfs-utils packages. 


NFS Servers : User : IP_Address

    dev-performance-la.procore.prod1 : diego : 10.1.31.152
    stage-web-la.procore.prod1-153 : goku : 10.1.31.153

AutoFS Server : IP_Address

    dev-app-la.procore.prod1 : 10.1.31.151
