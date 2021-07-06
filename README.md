# The Ambassador Pattern

Just like the **Sidecar** pattern, the Ambassador is a container that runs in the same Pod that the application container runs.

Basically, the Ambassador works as a proxy, it handles all the requests coming from the application.

![Basic Ambassador](./ambassador.png)

One of the main advantages of this pattern is that there is no need that the application container knows the external services URLs, he will always communicate through `localhost` with the Ambassador.

The Ambassador is responsible to `discover` the external service address (this process is also knows as `Service Discovery`).

---

## Examples

This repo contains two examples where the Ambassador pattern may be applied to.

### Sharded Redis

The first example is a sharded-redis:

- We have a `StatefulSet` defining 3 replicas of a `redis` container;
- Also, there is a `Service` called `redis-svc` to expose the `Pods` to the cluster;
- We're using [twemproxy](https://github.com/twitter/twemproxy) to act as a proxy to the redis containers;
- Lastly, we defined a `Pod` called `ambassador-example` that defines to pods:
  - `nginx` that is our "client" application that needs to communicate with the `redis`
  - `twemproxy` that is the Ambassador.

![Sharded Redis](./sharded-redis.png)