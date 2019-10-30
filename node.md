```
docker pull haproxy:6000/kube-proxy:v1.16.2
docker pull haproxy:6000/pause:3.1
docker pull haproxy:6000/calico_cni:v3.10.0
docker pull haproxy:6000/calico_pod2daemon-flexvol:v3.10.0
docker pull haproxy:6000/calico_node:v3.10.0
docker pull haproxy:6000/calico_kube-controllers:v3.10.0


docker tag haproxy:6000/kube-proxy:v1.16.2 k8s.gcr.io/kube-proxy:v1.16.2
docker tag haproxy:6000/pause:3.1 k8s.gcr.io/pause:3.1
docker tag haproxy:6000/calico_cni:v3.10.0 calico/cni:v3.10.0
docker tag haproxy:6000/calico_pod2daemon-flexvol:v3.10.0 calico/pod2daemon-flexvol:v3.10.0
docker tag haproxy:6000/calico_node:v3.10.0 calico/node:v3.10.0
docker tag haproxy:6000/calico_kube-controllers:v3.10.0 calico/kube-controllers:v3.10.0

```
```
mkdir /root/.ssh
chmod 700 /root/.ssh
scp root@master1:/root/.ssh/id_rsa.pub /root/.ssh/authorized_keys


mkdir -p $HOME/.kube
scp root@master1:$HOME/.kube/config $HOME/.kube/config
```

```
kubeadm token create --print-join-command
```