# Configuration pve-no-subscription

1. `nano /etc/apt/sources.list`
```yaml
# Proxmox VE pve-no-subscription repository provided by proxmox.com
# NOT recommended for production use
deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription

# Security updates
deb http://security.debian.org/debian-security bookworm-security main contrib
```
2. `nano /etc/apt/sources.list.d/ceph.sources`
```yaml
#Types: deb
#URIs: https://enterprise.proxmox.com/debian/ceph-squid
#Suites: trixie
#Components: enterprise
#Signed-By: /usr/share/keyrings/proxmox-archive-keyring.gpg

Types: deb
URIs: http://download.proxmox.com/debian/ceph-squid
Suites: trixie
Components: no-subscription
Signed-By: /usr/share/keyrings/proxmox-archive-keyring.gpg
```
3. `nano /etc/apt/sources.list.d/pve-enterprise.sources` 
```yaml
# Types: deb
# URIs: https://enterprise.proxmox.com/debian/pve
# Suites: trixie
# Components: pve-enterprise
# Signed-By: /usr/share/keyrings/proxmox-archive-keyring.gpg
# NO-SUB REPOSITORY
Types: deb
URIs: http://download.proxmox.com/debian/pve
Suites: trixie
Components: pve-no-subscription
Signed-By: /usr/share/keyrings/proxmox-archive-keyring.gpg
```

