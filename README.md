# rbaccollection

## Workshop 1.

##Create user jane that will have access to pod in her namespace only as reader. And no access outside of cluster

### 1. Create a kubernetes user with X509 Client Certs by accessing Kubernetes
Master and running commands below:

```
sudo openssl genrsa -out /tmp/jane-key.pem 2048
sudo openssl req -new -key /tmp/jane-key.pem -out /tmp/jane-csr.pem -subj '/CN=jane/O=some-group' 
sudo openssl x509 -req -in /tmp/jane-csr.pem -CA /etc/kubernetes/ssl/ca.pem -CAkey /etc/kubernetes/ssl/ca-key.pem -CAcreateserial -out /tmp/jane.pem -days 50
sudo kubectl config set-credentials jane --client-certificate=/tmp/jane.pem --client-key=/tmp/jane-key.pem
```

### 2. Create a pod reader Role and Bind it with jane user via RoleBinding

```
kubectl apply -f user_pod_reader.yaml
```
