```
docker pull haproxy:6000/kube-proxy:v1.16.0
docker pull haproxy:6000/pause:3.1
docker pull haproxy:6000/cni:v3.8.2
docker pull haproxy:6000/pod2daemon-flexvol:v3.8.2
docker pull haproxy:6000/kube-controllers:v3.8.2
docker pull haproxy:6000/node:v3.8.2


docker tag haproxy:6000/kube-proxy:v1.16.0 k8s.gcr.io/kube-proxy:v1.16.0
docker tag haproxy:6000/pause:3.1 k8s.gcr.io/pause:3.1
docker tag haproxy:6000/cni:v3.8.2 calico/cni:v3.8.2
docker tag haproxy:6000/pod2daemon-flexvol:v3.8.2 calico/pod2daemon-flexvol:v3.8.2
docker tag haproxy:6000/kube-controllers:v3.8.2 calico/kube-controllers:v3.8.2
docker tag haproxy:6000/node:v3.8.2 calico/node:v3.8.2

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