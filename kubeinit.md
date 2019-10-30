```
yum install -y git
```

关闭swap
```
swapoff -a
sed -i "s/\/dev\/mapper\/centos-swap/#\/dev\/mapper\/centos-swap/g" /etc/fstab
echo 'swapoff -a' >> /etc/profile
source /etc/profile
```

设置私有registry镜像地址（当网络无法访问公共镜像的时候）
```
export privateregistry=haproxy:6000
```

修改 docker pull 配置
```
cat > /etc/docker/daemon.json << EOF
{
    "bip": "172.31.0.1/16",
    "insecure-registries": [
        "$privateregistry"
    ]
}
EOF

systemctl daemon-reload && systemctl restart docker
```


添加hosts
```
cat >> /etc/hosts << EOF
30.0.0.11 haproxy

30.0.0.21 master1
30.0.0.22 master2
30.0.0.23 master3
30.0.0.24 master4
30.0.0.25 master5

30.0.0.31 node1
30.0.0.32 node2
30.0.0.33 node3
30.0.0.34 node4
30.0.0.34 node5
30.0.0.34 node6
30.0.0.34 node7
30.0.0.34 node8
30.0.0.34 node9

30.0.0.41 ingress1
30.0.0.42 ingress2
30.0.0.43 ingress3
30.0.0.44 ingress4
30.0.0.45 ingress5

30.0.0.51 ceph1
30.0.0.52 ceph2
30.0.0.53 ceph3

EOF

```


```
cat > /etc/sysctl.d/k8s.conf << EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
vm.swappiness=0
EOF

modprobe br_netfilter
sysctl -p /etc/sysctl.d/k8s.conf

cat > /etc/sysconfig/modules/ipvs.modules << EOF
#!/bin/bash
modprobe -- ip_vs
modprobe -- ip_vs_rr
modprobe -- ip_vs_wrr
modprobe -- ip_vs_sh
modprobe -- nf_conntrack_ipv4
EOF

chmod 755 /etc/sysconfig/modules/ipvs.modules && bash /etc/sysconfig/modules/ipvs.modules && lsmod | grep -e ip_vs -e nf_conntrack_ipv4

yum install -y ipvsadm ipset

```

```
cat << EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=http://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=0
repo_gpgcheck=0
gpgkey=http://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg http://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
EOF
```
```
yum makecache fast
yum install -y kubelet kubeadm kubectl
```
```
echo  'Environment="KUBELET_CGROUP_ARGS=--cgroup-driver=cgroupfs"' >> /usr/lib/systemd/system/kubelet.service.d/10-kubeadm.conf

sed -i "s/=/=--fail-swap-on=false --node-status-update-frequency=4s/g" /etc/sysconfig/kubelet
systemctl enable kubelet && systemctl start kubelet && systemctl status kubelet



git clone https://github.com/zhangjiongdev/kubeadm116.git

mv /usr/bin/kubeadm /usr/bin/kubeadm_bak

mv kubeadm116/kubeadm /usr/bin/kubeadm
chmod +x /usr/bin/kubeadm

mv kubeadm116/calico.yaml calico.yaml
mv kubeadm116/kubeadm-init.yaml kubeadm-init.yaml


```
