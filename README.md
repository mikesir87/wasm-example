# Lightweight and secure microservice with a database backend

In this repo, we demonstrate a microservice written in Rust, and connected to a MySQL database. It supports CURD operations on a database table via a HTTP service interface. The microservice is compiled into WebAssembly and runs in the WasmEdge Runtime, which is a secure and lightweight alternative to natively compiled Rust apps in Linux containers. The WasmEdge Runtime can be managed and orchestrated by container tools such as the Docker CLI, Podman, as well as almost all flavors of Kubernetes. It also works with microservice management frameworks such as Dapr.

> Everything described in this document is captured in the [GitHub Actions CI workflow](.github/workflows/ci.yml).


## Test with Docker

Using a version of Docker with Wasm WASI support, start the example stack using `docker compose`:

```bash
docker compose up
```

Initialize the database using the `/init` endpoint:

```bash
docker run --rm --network host curlimages/curl curl http://localhost:8080/init
```

List the current orders using the `/orders` endpoint:

```bash
docker run --rm --network host curlimages/curl curl http://localhost:8080/orders
```

Add the example orders:

```bash
cat orders.json | docker run --rm --network host -i curlimages/curl curl http://localhost:8080/create_orders -X POST -d @-
```
