SSD and Active Directory on  Ubuntu 20.04.1 LTS
=====
https://ubuntu.com/server/docs/service-sssd


1. Install 

\# sudo apt install sssd-ad sssd-tools realmd adcli

2. map the dc in file /etc/hosts and set the DC as nameserver in netplan

\# echo "x.x.x.x lab.private" >> /etc/hosts

netplan:

\# vi /etc/netplan/00-installer-config.yaml


\# This is the network config written by 'subiquity'
network:
  ethernets:
    ens160:
      addresses:
      - 10.x.x.x/24
      gateway4: 10.x.x.1
      nameservers:
        addresses:
        - **10.x.x.x**
  version: 2
  
\# netplan apply

test resolution:

\# dig -t SRV _ldap._tcp.lab.private @lab.private



3. discover the domain before join

\# realm -v discover lab.private


\* Resolving: _ldap._tcp.lab.private
\* Resolving: lab.private
\* Performing LDAP DSE lookup on: 10.39.132.130
\* Successfully discovered: lab.private
lab.private
  type: kerberos
  realm-name: LAB.PRIVATE
  domain-name: lab.private
  configured: no
  server-software: active-directory
  client-software: sssd
  required-package: sssd-tools
  required-package: sssd
  required-package: libnss-sss
  required-package: libpam-sss
  required-package: adcli
  required-package: samba-common-bin
  
  4. join the domain using administrator@lab.private password
  
  \# realm -v join lab.private
  
  5. after the jon check again with the discovery
  
\# realm discover lab.private

lab.private
  type: kerberos
  realm-name: LAB.PRIVATE
  domain-name: lab.private
  configured: kerberos-member
  server-software: active-directory
  client-software: sssd
  required-package: sssd-tools
  required-package: sssd
  required-package: libnss-sss
  required-package: libpam-sss
  required-package: adcli
  required-package: samba-common-bin
  login-formats: %U@lab.private
  login-policy: allow-realm-logins
  

6. run pam auto update to have the homedir automatic creation at login-formats

\# pam-auth-update --enable mkhomedir

7. check if is working fine

\# id USERNAME@lab.private

uid=17401106(USERNAME@lab.private) gid=17400513(domain USERNAME@lab.private) groups=17400513(domain users@lab.private)

8. check login

\# login USERNAME@lab.private



  
  