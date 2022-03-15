# Fedora CoreOS

Lets go

```bash
# Convert from bu to ign
podman run --interactive --rm quay.io/coreos/butane:release \
    --pretty --strict < test.bu.yaml > transpiled_config.ign

# Simple server to share file
python3 -m http.server


curl 192.168.86.53:8000/transpiled_config.ign

# Get drive
lsblk

# Install core os
sudo coreos-installer install /dev/vda \
    -I http://192.168.86.53:8000/transpiled_config.ign --insecure-ignition


# Generate password
podman run -ti --rm quay.io/coreos/mkpasswd --method=yescrypt
```

```bash
sudo rpm-ostree install https://github.com/k3s-io/k3s-selinux/releases/download/v1.1.stable.1/k3s-selinux-1.1-1.el8.noarch.rpm

sudo reboot

sudo curl -sfL https://get.k3s.io | sh -s - --write-kubeconfig-mode 644
```
