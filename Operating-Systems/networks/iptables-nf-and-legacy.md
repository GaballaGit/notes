3/13/26

# IPTABLES - nftables and legacy


On my way to setup KubeVirt, I ran into an issue when trying to create the cluster when getting started:

```md

 ++ seq 1 0
8 + iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
q iptables v1.8.11 (legacy): can't initialize iptables table `nat': Table does not exist (do you need to insmod?)
7 Perhaps iptables or your kernel needs to be upgraded.

```
