# Dockerfile

It is a series of instructions to build a container with versioning

```
docker build .
docker run <ID>
docker build . --tag my-node-app ## or -t instead of --tag
docker run my-node-app
docker build -t my-node-app:1 .
docker run my-node-app:1
docker build -t my-node-app:2 .
docker run my-node-app:2
docker run my-node-app:1
```