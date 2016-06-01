# docker-haproxy
HAProxy docker container based on alpine linux. Uses Confd and Etcd for automatic configuration. Minimal downtime updates.

**Warning: Not production ready (yet)!**

# Based on / inspired by:
* [HAProxy-Confd](https://hub.docker.com/r/yaronr/haproxy-confd/)

# Build
docker build -t cnares/docker-haproxy:latest github.com/chinaares/docker-haproxy

# Configure Evn
curl "http://192.166.69.38:2379/v2/keys/haproxy-discover/services/myapp/domain"  -X PUT -d value="example.org"
curl "http://192.166.69.38:2379/v2/keys/haproxy-discover/services/myapp/upstreams/nodeA"  -X PUT -d value="192.168.99.100:32840"
curl "http://192.166.69.38:2379/v2/keys/haproxy-discover/services/myapp/upstreams/nodeB"  -X PUT -d value="192.168.99.100:32838"
curl "http://192.166.69.38:2379/v2/keys/haproxy-discover/services/myapp/upstreams/nodeC"  -X PUT -d value="192.168.99.100:32839"


# Run

ETCD_NODE=192.166.69.38:2379

Interactive:
docker run -it --rm -e ETCD_NODE=$ETCD_NODE daocloud.io/cnares/docker-haproxy /bin/bash
Non-interactive:
docker run -d  -p :8080 -p :9000 -e ETCD_NODE=$ETCD_NODE daocloud.io/cnares/docker-haproxy


