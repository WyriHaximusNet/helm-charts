# Redis Database Assignment Operator

<p align="center">
  <img src="https://helm.wyrihaximus.net/images/charts/redis-db-assignment-operator.png">
</p>

Opinionated helm chart for [`wyrihaximusnet/docker-kubernetes-redis-db-assignment-operator`](https://github.com/WyriHaximusNet/docker-kubernetes-redis-db-assignment-operator).

## Configuration

No configuration required!

## Example use

The following definition will create a redis-database resource on your cluster. The operator picks it up and finds a 
redis database that isn't in use according to the operators internal state.

```yaml
apiVersion: wyrihaximus.net/v1
kind: RedisDatabase
metadata:
  name: example
spec:
  secret:
    name: example-redis-database
  service:
    read: redis://redis-follower.redis.svc.cluster.local:6379/
    write: redis://redis-leader.redis.svc.cluster.local:6379/
```

The resulting secret looks like this:

```yaml
apiVersion: v1
kind: Secret
type: Opaque
metadata:
  name: example-redis-database
  namespace: default
data:
  DATABASE: BASE64_ENCODED
  READ: BASE64_ENCODED
  WRITE: BASE64_ENCODED
```

## Opinionated decisions

* State is stored in a hardcoded configmap named `redis-database-assignment-operator-in-use-dbs-list` in the namespace the operator resides in.
