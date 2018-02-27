# kubernetes auth

### X509 Client Cert 
先使用 hack/local-up-cluster.sh 启动集群，然后再关闭只启动 kube-apiserver, 下面是 启动 x509  Client Cert 认证时的一些必传参数。
```Bash
sudo ./kube-apiserver --cert-dir="/var/run/kubernetes" --client-ca-file="/var/run/kubernetes/client-ca.crt" --etcd-servers=http://localhost:2380 --tls-cert-file="/var/run/kubernetes/serving-kube-apiserver.crt" --tls-private-key-file="/var/run/kubernetes/serving-kube-apiserver.key" -v 1
```

客户端验证证书
```bash
➜  kubernetes git:(master) ✗ curl -k -X POST --key /var/run/kubernetes/client-admin.key --cert /var/run/kubernetes/client-admin.crt -H 'Content-Type: application/json' --data '{"spec":{"namespace":"kube-system"}}' https://localhost:6443/apis/authorization.k8s.io/v1/selfsubjectrulesreviews
{
  "kind": "SelfSubjectRulesReview",
  "apiVersion": "authorization.k8s.io/v1",
  "metadata": {
    "creationTimestamp": null
  },
  "spec": {
    
  },
  "status": {
    "resourceRules": [
      {
        "verbs": [
          "*"
        ],
        "apiGroups": [
          "*"
        ],
        "resources": [
          "*"
        ]
      }
    ],
    "nonResourceRules": [
      {
        "verbs": [
          "*"
        ],
        "nonResourceURLs": [
          "*"
        ]
      }
    ],
    "incomplete": false
  }
}
```