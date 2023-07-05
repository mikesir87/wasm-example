# Lightweight and secure microservice with a database backend

In this repo, we demonstrate a simple http server written in Rust. The server is compiled into WebAssembly and runs in the WasmEdge Runtime, which is a secure and lightweight alternative to natively compiled Rust apps in Linux containers. The WasmEdge Runtime can be managed and orchestrated by container tools such as the Docker CLI, Podman, as well as almost all flavors of Kubernetes. It also works with microservice management frameworks such as Dapr.

> Everything described in this document is captured in the [GitHub Actions build workflow](.github/workflows/build.yml).


## Test with Docker

Using a version of Docker with Wasm WASI support, start the example stack using `docker compose`:

```bash
docker compose up
```

Get the server's root endpoint:

```bash
docker run --rm --network host curlimages/curl curl -sw'\n' http://localhost:8080/
```

Post to the server's `/echo` endpoint:

```bash
docker run --rm --network host curlimages/curl curl -sw'\n' -X POST -d 'hello world' http://localhost:8080/echo
```
