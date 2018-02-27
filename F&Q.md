# F&Q

### Mac 下验证 x509 Client Certs 认证方式的时候传证书报错

```bash
➜  kubernetes git:(master) ✗ curl -X POST --key /var/run/kubernetes/client-admin.key --cert /var/run/kubernetes/client-admin.crt -H 'Content-Type: application/json' https://localhost:6443/apis/authorization.k8s.io/v1/selfsubjectaccessreviews --data '{"spec":{"namespace":"kube-system"}}'
curl: (58) SSL: Can't load the certificate "/var/run/kubernetes/client-admin.crt" and its private key: OSStatus -25299```
```
#####  使用下面命令修复
```bash
brew install curl --with-openssl
brew link curl --force
hash -r```
```
##### 相关 issue
- https://github.com/boot2docker/boot2docker/issues/573#issuecomment-254436739