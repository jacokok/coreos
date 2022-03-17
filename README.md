# Fedora CoreOS

## Lets go

```bash
# Convert from bu to ign
podman run --interactive --rm quay.io/coreos/butane:release --pretty --strict < config.yaml > config.ign

# Simple server to share file
python3 -m http.server

# Get drive
lsblk

# Install core os
sudo coreos-installer install /dev/vda -I http://192.168.86.53:8000/config.ign --insecure-ignition

sudo coreos-installer install /dev/nvme0n1 -I https://raw.githubusercontent.com/jacokok/coreos/main/config.ign

# Generate password
podman run -ti --rm quay.io/coreos/mkpasswd --method=yescrypt
```

## Post Install Script

```bash
#https://github.com/k3s-io/k3s-selinux
sudo rpm-ostree install https://github.com/k3s-io/k3s-selinux/releases/download/v1.1.stable.1/k3s-selinux-1.1-1.el8.noarch.rpm

sudo reboot

sudo curl -sfL https://get.k3s.io | sh -s - --write-kubeconfig-mode 644

sudo curl -sfL https://get.k3s.io | K3S_TOKEN= K3S_URL=https://192.168.86.40:6443 sh -

kubectl label nodes server2 gitpod.io/workload_meta=true
```
