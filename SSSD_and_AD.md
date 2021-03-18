SSD and Active Directory on  Ubuntu 20.04.1 LTS
=====
https://ubuntu.com/server/docs/service-sssd


>1. Install 

\# sudo apt install sssd-ad sssd-tools realmd adcli

>2. map the dc in file /etc/hosts and set the DC as nameserver in netplan

\# echo "x.x.x.x lab.private" >> /etc/hosts

netplan:

\# vi /etc/netplan/00-installer-config.yaml


\# This is the network config written by 'subiquity' <br>
network:<br>
  ethernets:<br>
    ens160:<br>
      addresses:<br>
      - 10.x.x.x/24<br>
      gateway4: 10.x.x.1<br>
      nameservers:<br>
        addresses:<br>
        - **10.x.x.x**<br>
  version: 2<br>
  
\# netplan apply

test resolution:

\# dig -t SRV _ldap._tcp.lab.private @lab.private



>3. discover the domain before join

\# realm -v discover lab.private


\* Resolving: _ldap._tcp.lab.private<br>
\* Resolving: lab.private<br>
\* Performing LDAP DSE lookup on: 10.39.132.130<br>
\* Successfully discovered: lab.private<br>
lab.private<br>
  type: kerberos<br>
  realm-name: LAB.PRIVATE<br>
  domain-name: lab.private<br>
  configured: no<br>
  server-software: active-directory<br>
  client-software: sssd<br>
  required-package: sssd-tools<br>
  required-package: sssd<br>
  required-package: libnss-sss<br>
  required-package: libpam-sss<br>
  required-package: adcli<br>
  required-package: samba-common-bin<br>
  
>4. join the domain using administrator@lab.private password
  
  \# realm -v join lab.private
  
>5. after the jon check again with the discovery
  
\# realm discover lab.private

lab.private<br>
  type: kerberos<br>
  realm-name: LAB.PRIVATE<br>
  domain-name: lab.private<br>
  configured: kerberos-member<br>
  server-software: active-directory<br>
  client-software: sssd<br>
  required-package: sssd-tools<br>
  required-package: sssd<br>
  required-package: libnss-sss<br>
  required-package: libpam-sss<br>
  required-package: adcli<br>
  required-package: samba-common-bin<br>
  login-formats: %U@lab.private<br>
  login-policy: allow-realm-logins<br>
  

>6. run pam auto update to have the homedir automatic creation at login-formats

\# pam-auth-update --enable mkhomedir

>7. check if is working fine

\# id USERNAME@lab.private

uid=17401106(USERNAME@lab.private) gid=17400513(domain USERNAME@lab.private) groups=17400513(domain users@lab.private)

>8. check login

\# login USERNAME@lab.private


>9. configure SSSD to use short login without domain

in sssd.conf comment:

use_fully_qualified_names = True

and add:

use_fully_qualified_names = False





  
  