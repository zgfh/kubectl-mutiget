# kubectl-mutiget
一个简单的脚本方便一次性查看多个集群的资源

## 安装
复制 kubectl-mutiget 文件 到/bin下即可
例如
```
wget -O /bin/kubectl-mutiget https://raw.githubusercontent.com/zgfh/kubectl-mutiget/main/kubectl-mutiget
chmod +x /bin/kubectl-mutiget
```



## 使用
1. 设置集群
默认通过contexts 查询到几个集群，就会返回几个集群的结果
```
kubectl config get-contexts
CURRENT   NAME                 CLUSTER              AUTHINFO             NAMESPACE
*         kind-kind-k8s-1-15   kind-kind-k8s-1-15   kind-kind-k8s-1-15
          kind-kind-k8s-1-18   kind-kind-k8s-1-18   kind-kind-k8s-1-18
          kind-kind-k8s-1-23   kind-kind-k8s-1-23   kind-kind-k8s-1-23
```
如果你想设定具体的那几个集群，可以定义一个 MUTIGET_CONTEXT 变量(空格隔开)
```
export MUTIGET_CONTEXT="kind-kind-k8s-1-15 kind-kind-k8s-1-18"
```

2. 查询
和`kubectl get xxx`用法几乎一样，替换成`kubectl mutiget xxx`即可，这样获取到的就是`kubectl config `

```
➜  ~ kubectl mutiget pod
---------- cluster: kind-kind-k8s-1-15 ----------
NAME                     READY   STATUS    RESTARTS   AGE
test2-6d4f84cbf9-grrhn   1/1     Running   0          3h11m
test2-6d4f84cbf9-xltd9   1/1     Running   0          3h11m
---------- cluster: kind-kind-k8s-1-18 ----------
No resources found in default namespace.
---------- cluster: kind-kind-k8s-1-23 ----------
NAME                     READY   STATUS    RESTARTS   AGE
test2-5fb85989fd-r2nfr   1/1     Running   0          22m
```
