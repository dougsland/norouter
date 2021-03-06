
---
title: "Examples"
linkTitle: "Examples"
weight: 3
description: >
  Examples for Docker, Podman, Kubernetes, LXD, SSH, ...
---

The following example contains configurations for Docker, Kubernetes, LXD, and SSH in a single YAML file.

```yaml
# Example manifest for NoRouter.
# Run `norouter <FILE>` to start NoRouter with the specified manifest file.
#
# The `norouter` binary needs to be installed on all the remote hosts.
# Run `norouter show-installer` to show the installation script.
#
hosts:
# localhost
  local:
    vip: "127.0.42.100"
# Docker & Podman container (docker exec, podman exec)
# The cmd string can be also written as a string slice: ["docker", "exec", "-i", "some-container", "norouter"]
  docker:
    cmd: "docker exec -i some-container norouter"
    vip: "127.0.42.101"
    ports: ["8080:127.0.0.1:80"]
# Writing /etc/hosts is possible on most Docker and Kubernetes containers
    writeEtcHosts: true
# Kubernetes Pod (kubectl exec)
  kube:
    cmd: "kubectl --context=some-context exec -i some-pod -- norouter"
    vip: "127.0.42.102"
    ports: ["8080:127.0.0.1:80"]
# Writing /etc/hosts is possible on most Docker and Kubernetes containers
    writeEtcHosts: true
# LXD container (lxc exec)
  lxd:
    cmd: "lxc exec some-container -- norouter"
    vip: "127.0.42.103"
    ports: ["8080:127.0.0.1:80"]
# SSH
# If your key has a passphrase, make sure to configure ssh-agent so that NoRouter can login to the remote host automatically.
  ssh:
    cmd: "ssh some-user@some-ssh-host.example.com -- norouter"
    vip: "127.0.42.104"
    ports: ["8080:127.0.0.1:80"]

```

The example can be also shown by running `norouter show-example`, or by running `norouter --open-editor`.
