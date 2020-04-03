```
[root@master ~]# mkdir RBAC
[root@master ~]# cd RBAC
```
```
[root@master RBAC]# kubectl create namespace finance
namespace/finance created
```
```
[root@master RBAC]# kubectl get ns
NAME              STATUS   AGE
default           Active   15d
finance           Active   9s
kube-node-lease   Active   15d
kube-public       Active   15d
kube-system       Active   15d
mynamespace       Active   43m
```
```
[root@master RBAC]# openssl genrsa -out user1.key 2048
Generating RSA private key, 2048 bit long modulus
.............................................+++
................................+++
e is 65537 (0x10001)
[root@master RBAC]# cat user1.key
-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAot+uySMlgu/n89MijMrwi9Q/tmwqygPK+y42PL3zwtk02z74
eNePlPVnVTmnTGysOSuk36H6VyP3Jp1bowqKCS0Rinmv64NWdaUnd3b6ardlD6E5
NJgrt3zhJ8xIaplpI5sXQ92xGhz8B/DuJZ6n4cnDhnbuwu85XckkKQ2rKEPcBQeq
GB7EZSICosMjphm+ZslB43bxEWoogq/ZwIP4DyOX0QGYmVNCPcY94XECHE+4mJUQ
4smhsi362S1bSYQRQ4wYbUWt+Uc+zY7RuOaM6PEfmZCmM4xLNj7rbIkESTnXd54B
O28nVhcib2TUB5zkt/5m3dtdVNYjU3+v4VTAwwIDAQABAoIBAQCGcLyFqk08V2rP
CGhsbtc/lGNC4OYw+hCCZRK/8MtU+pV2o/PVS5lpC2fQIVbG7qz6Q9xD/B/37egE
J7+MRRbLnDfuZaOgczjawwhgxATQMbFpxVrC3xi2zI3NnAHqe9cdXNdHXabiNyqS
I31v8BYDede7FlDe9zgTAgSnHnE5Ofip0u8UxS5WINJQ504+ZptXF7xR6gMmzKIo
IRasA+BFnOj0p1SgUS8GTZmK4N/UWJF36LVR8/XaP5hZFtb46Q13mpbDVP0Bnf0H
pg9zZh7b1gAP68P1bFRZAqvVLSSObeV17kwMI8JnqXjaFmxX8zZi7UmRnfFsRDFI
qhwFRxiBAoGBANhMWdoxtixaq5FdZbhZmQhI7Rf/1CfHd69CBiJAumM2MNC8gnWM
Ah4VETaZWnVYO6Fg4ZE5J20anmPBKMTLUGXjrBM4fieX25l6XUmYz3G0B2MOczsy
je83uCnirTfIeOjz/dwwYky7611U7MDFreb1ZnB24IECzPZcfuoeguXvAoGBAMDE
90qZ6frfwxqka5URWDt3MRoriYxoibbdJ7dJJTeE1v8HF+PxgFDyvJnUfojhMJvL
1OcxgIzPpD+szl/AJsRvDl305ObQJI3AD2zl6b2vx3S8RnA5BeKEvWakA6fgctlL
k7e72dPPMUt8Em6n7UHzytxvukJqKb7jCRRIXsZtAoGBAIK+zEV/bS4sdK7+9ODV
kBKY+nBaXSTahvcygsCrvb8A38sdWAKz6gfDFk+ZrTtnZUwsYs1E7hceUwXbmcgz
WdrtH3PS3zcRrVV9yOwW6bZCa4CuGGt9KJykYrc25RvmG2g9LIOv34ugwCn/jskL
9Q254v0yboytY7W7vZ/JZ7iTAoGABcbhUk8CgA4snqPGxZTbfAy6X/pmCNspJV3D
Tu7WOq+0cbgYszANlF9x33pKwHdfKYwWOUd2fsHKPk5DcQMlJkXdvFsWcQRT1Bup
Wq4ZLyIRbCIoSjyrPHqV4nmP0nwbdP+a0arDgGF5LLXvJ3nI1m0j6y89+beMwLe1
EfKJRJECgYEAnEXaSiGQc9csq+/hJqLSVJ5Xu4haHEZFarOZ0Jv2c0Aj0aXwnMvi
nSTs0K1Z/OHo2/GH7zXc4pt5cCBhh8QZdc5uMR29W7ENUPe6iwbtR1P5nd/71ois
Z5mJaTsrV6HQhWP2T1P0nbfLLfe6LzqfUH2Bs4ho6Fvujh9U2ag7fKs=
-----END RSA PRIVATE KEY-----
```
```
[root@master RBAC]# openssl req -new -key user1.key -out user1.csr -subj "/CN=user1/O=finance"
Subject Attribute 0 has no known NID, skipped
[root@master RBAC]# ls
user1.csr  user1.key
```
```
[root@master RBAC]# cd /etc/kubernetes/pki
[root@master pki]# ls
apiserver.crt              apiserver.key                 ca.crt  front-proxy-ca.crt      front-proxy-client.key
apiserver-etcd-client.crt  apiserver-kubelet-client.crt  ca.key  front-proxy-ca.key      sa.key
apiserver-etcd-client.key  apiserver-kubelet-client.key  etcd    front-proxy-client.crt  sa.pub
[root@master pki]# 
```
```
[root@master pki]# cp ca.crt /root/RBAC
[root@master pki]# cp ca.key /root/RBAC
```
```
[root@master RBAC]# ls
ca.crt  ca.key  user1.csr  user1.key
[root@master RBAC]# 
```

```
[root@master RBAC]# openssl x509 -req -in user1.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out user1.crt -days 365
Signature ok
subject=/CN=user1
Getting CA Private Key
[root@master RBAC]# ls
ca.crt  ca.key  ca.srl  user1.crt  user1.csr  user1.key
[root@master RBAC]# 
```
```
[root@master ~]# bash
[root@master ~]# kubectl config view
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://192.168.152.169:6443
  name: kubernetes
contexts:
- context:
    cluster: kubernetes
    namespace: mynamespace
    user: kubernetes-admin
  name: kubernetes-admin@kubernetes
current-context: kubernetes-admin@kubernetes
kind: Config
preferences: {}
users:
- name: kubernetes-admin
  user:
    client-certificate-data: REDACTED
    client-key-data: REDACTED
[root@master ~]# 

```

###### From above we see a couple of generated files - ca.crt, ca.key, ca.srl, user1.crt, user1.csr, user1.key; out of which we need to share (ca.crt, user1.crt, user1.key) to user1 to setup his kubeconfig to access this K8 Cluster.

```
[root@master RBAC]#  kubectl --kubeconfig user1.kubeconfig config set-cluster kubernetes --server https://192.168.152.169:6443 --certificate-authority=ca.crt
Cluster "kubernetes" set.
[root@master RBAC]#  
```
```
[root@master RBAC]# kubectl --kubeconfig user1.kubeconfig config set-credentials user1 --client-certificate user1.crt --client-key user1.key
User "user1" set.
[root@master RBAC]# kubectl --kubeconfig user1.kubeconfig config set-context user1-kubernetes --cluster kubernetes --namespace finance --user user1
Context "user1-kubernetes" created.
[root@master RBAC]# ls
ca.crt  ca.key  ca.srl  user1.crt  user1.csr  user1.key  user1.kubeconfig
[root@master RBAC]# 
```
```
[root@master RBAC]# sudo gedit user1.kubeconfig
Change current-context from "" to current-context: "user1-kubernetes"

```
```
[root@master RBAC]# cp user1.kubeconfig ~/.kube/config
cp: overwrite ‘/root/.kube/config’? no 
```
###### [above] We chose 'No' because I am using one machine for both 'user1' and 'admin'
```
[root@master RBAC]# kubectl --kubeconfig user1.kubeconfig get pods
Error from server (Forbidden): pods is forbidden: User "user1" cannot list resource "pods" in API group "" in the namespace "finance"
[root@master RBAC]# 
```
<hr>
### Authorizaation:

##### Create a Role:
```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  creationTimestamp: "2020-04-03T21:31:21Z"
  managedFields:
  - apiVersion: rbac.authorization.k8s.io/v1
    fieldsType: FieldsV1
    fieldsV1:
      f:rules: {}
    manager: kubectl
    operation: Update
    time: "2020-04-03T21:31:21Z"
  name: user1-role-finance
  namespace: finance
  resourceVersion: "8732"
  selfLink: /apis/rbac.authorization.k8s.io/v1/namespaces/finance/roles/user1-role-finance
  uid: ed60223d-994f-4400-8237-027b386ba301
rules:
- apiGroups:
  - ""
  resources:
  - pods
  verbs:
  - get
  - list

```
 OR
```
kubectl -n finance get role user1-role-finance -o yaml
```
##### Now create RoleBinding:
```
[root@master RBAC]# kubectl -n finance get rolebinding user1-rolebinding-finance -o yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  creationTimestamp: "2020-04-03T21:37:29Z"
  managedFields:
  - apiVersion: rbac.authorization.k8s.io/v1
    fieldsType: FieldsV1
    fieldsV1:
      f:roleRef:
        f:apiGroup: {}
        f:kind: {}
        f:name: {}
      f:subjects: {}
    manager: kubectl
    operation: Update
    time: "2020-04-03T21:37:29Z"
  name: user1-rolebinding-finance
  namespace: finance
  resourceVersion: "9571"
  selfLink: /apis/rbac.authorization.k8s.io/v1/namespaces/finance/rolebindings/user1-rolebinding-finance
  uid: 80f309ab-614b-413b-9f12-99e774a0ebd3
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: user1-role-finance
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: User
  name: user1
[root@master RBAC]# 

```
OR
```
kubectl create rolebinding user1-rolebinding-finance --role=user1-role-finance --user=user1 --namespace finance
```

#### TRY:
```
[root@master RBAC]# kubectl --kubeconfig user1.kubeconfig get pods
No resources found in finance namespace.
[root@master RBAC]# 
```

