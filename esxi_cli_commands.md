ESXi cli commands
=====

>List all vm on an host

\# esxcli vm process list

> search for a specific vm 

\# esxcli vm process list \| grep -i VMNAME

>Kill vm on an host with World ID

\# esxcli vm process kill –type=[soft,hard,force] –world-id=WorldNumber
\# esxcli vm process kill -t soft -w WorldNumber

Three power-off methods are available:<br>
*Soft* is the most graceful, *hard* performs an immediate shutdown, and *force* should be used as a last resort.

>Check build and version number

\# esxcli system version get

>Installation date

\# esxcli system stats installtime get

>List installed VIBS, a VIB \(VMware Installation Bundle) is a software package that gets installed on a vSphere ESXi host that contains things like drivers

\# esxcli software vib list

>List all datastore connected to the host

\#esxcli storage filesystem list

