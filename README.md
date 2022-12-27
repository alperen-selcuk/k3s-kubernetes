# k3s-kubernetes

nginx config

```
load_module '/usr/lib/nginx/modules/ngx_stream_module.so';

worker_processes 4;
worker_rlimit_nofile 40000;

events {
    worker_connections 8192;
}

stream {
    upstream k3snodes {
        least_conn;
        server <your master ip>:6443 max_fails=3 fail_timeout=5s;
    }
    server {
        listen 6443;
        proxy_pass k3snodes;
    }
}
```

k3sup install

```
curl -sLS https://get.k3sup.dev | sh
sudo install k3sup /usr/local/bin/
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
