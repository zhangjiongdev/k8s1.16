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
ssh-keygen -t rsa
```


```
curl -O https://docs.projectcalico.org/v3.8/manifests/calico.yaml
```

```
https://github.com/zhangjiongdev/k8s1.16/blob/master/kubeadm-init.yaml
vi kubeadm-init.yaml

kubeadm init --config kubeadm-init.yaml
```



```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```



```
kubectl apply -f calico.yaml
```
