
```

k3sup install

```
curl -sLS https://get.k3sup.dev | sh
```

k3sup configuration

```
export SERVER=<your master ip>
export WORKER_1=<worker 1 ip>
export WORKER_2=<worker 2 ip>
export TLS_DOMAIN=<your domain>


k3sup install --cluster --host $SERVER --user root --tls-san $TLS_DOMAIN 

k3sup join --user root --ip $WORKER_1 --server-ip $SERVER --server-user root

k3sup join --user root --ip $WORKER_2 --server-ip $SERVER --server-user root
```
