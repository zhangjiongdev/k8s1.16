```
docker pull haproxy:6000/kube-apiserver:v1.16.2
docker pull haproxy:6000/kube-scheduler:v1.16.2
docker pull haproxy:6000/kube-proxy:v1.16.2
docker pull haproxy:6000/kube-controller-manager:v1.16.2-b

docker pull haproxy:6000/etcd:3.3.15-0
docker pull haproxy:6000/pause:3.1
docker pull haproxy:6000/coredns:1.6.2

docker pull haproxy:6000/calico_cni:v3.10.0
docker pull haproxy:6000/calico_pod2daemon-flexvol:v3.10.0
docker pull haproxy:6000/calico_node:v3.10.0
docker pull haproxy:6000/calico_kube-controllers:v3.10.0





docker tag haproxy:6000/kube-apiserver:v1.16.2 k8s.gcr.io/kube-apiserver:v1.16.2
docker tag haproxy:6000/kube-scheduler:v1.16.2 k8s.gcr.io/kube-scheduler:v1.16.2
docker tag haproxy:6000/kube-proxy:v1.16.2 k8s.gcr.io/kube-proxy:v1.16.2
docker tag haproxy:6000/kube-controller-manager:v1.16.2-b k8s.gcr.io/kube-controller-manager:v1.16.2

docker tag haproxy:6000/etcd:3.3.15-0 k8s.gcr.io/etcd:3.3.15-0
docker tag haproxy:6000/pause:3.1 k8s.gcr.io/pause:3.1
docker tag haproxy:6000/coredns:1.6.2 k8s.gcr.io/coredns:1.6.2

docker tag haproxy:6000/calico_cni:v3.10.0 calico/cni:v3.10.0
docker tag haproxy:6000/calico_pod2daemon-flexvol:v3.10.0 calico/pod2daemon-flexvol:v3.10.0
docker tag haproxy:6000/calico_node:v3.10.0 calico/node:v3.10.0
docker tag haproxy:6000/calico_kube-controllers:v3.10.0 calico/kube-controllers:v3.10.0

```


```
mkdir /root/.ssh
chmod 700 /root/.ssh
scp root@master1:/root/.ssh/id_rsa.pub /root/.ssh/authorized_keys

mkdir -p /etc/kubernetes/pki/etcd
scp root@master1:/etc/kubernetes/pki/\{ca.*,sa.*,front-proxy-ca.*\} /etc/kubernetes/pki/
scp root@master1:/etc/kubernetes/pki/etcd/ca.* /etc/kubernetes/pki/etcd/
scp root@master1:/etc/kubernetes/admin.conf /etc/kubernetes/

mkdir -p $HOME/.kube
scp root@master1:$HOME/.kube/config $HOME/.kube/config
```

生成加入集群的命令行
```
cmd=`kubeadm token create --print-join-command`
cmdstr=" --control-plane"
echo $cmd$cmdstr

```