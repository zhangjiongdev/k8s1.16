设置私有registry镜像地址（当网络无法访问公共镜像的时候）
```
export privateregistry=haproxy:5000
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


