# Kubernets积累

### 非root用户使用kubectl docker

```bash
# 添加docker权限
sudo usermod -a -G docker dong

# 添加kubectl使用权限
su - dong
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown dong:dong $HOME/.kube/config

# 配置环境变量 并使用source生效
export KUBECONFIG=/home/dong/.kube/config
```

