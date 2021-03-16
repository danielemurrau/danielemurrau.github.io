ESXi cli commands
=====

>List all vm on an host

\# esxcli vm process list

> search for a specific vm 

\# esxcli vm process list \| grep -i VMNAME

>Kill vm on an host with World ID

\# esxcli vm process kill –type=[soft,hard,force] –world-id=WorldNumber