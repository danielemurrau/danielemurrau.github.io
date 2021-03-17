SSD and Active Directory on  Ubuntu 20.04.1 LTS
=====
https://ubuntu.com/server/docs/service-sssd

1. Install 

\# sudo apt install sssd-ad sssd-tools realmd adcli

2. map the dc in file /etc/hosts 

\# echo "x.x.x.x lab.private" >> /etc/hosts

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
  


  
  