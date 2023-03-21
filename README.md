# vm
machines virtuelles

Ma vm slave de celle d'enzo

/etc/ansible/ ansible.cfg :
```
[defaults]
filehost=hosts
``` 

/etc/ansible/ hosts :
```
[server]
sysadmin@172.25.192.9
``` 

playbook utilisé
```
---
- hosts: server
  become: true
  - name: Génération de certificat auto-signé
      openssl_certificate:
        path: /etc/ssl/crt/gand1.fr.crt
        privatekey_path: /etc/ssl/private/gand1.fr.pem
        csr_path: /etc/ssl/csr/gand1.fr.csr
        provider: selfsigned

    - name: Génération d'un certificat signé avec une AC
      openssl_certificate:
        path: /etc/ssl/crt/gand1.fr.crt
        csr_path: /etc/ssl/csr/gand1.fr.csr
        ownca_path: /etc/ssl/crt/gand1_CA.crt
        ownca_privatekey_path: /etc/ssl/private/gand1_CA.pem
        provider: ownca
``` 
