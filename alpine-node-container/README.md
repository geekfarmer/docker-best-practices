# Create our own alpine container! (Recommended)

# Multi Stage containers (Just a little bit optimization)
We need `npm` to build the app, we don't need it to run the app. We can achieve elimination of npm from final container using Docker mulit-stage builds.

1. One container to build the app
2. Another container to run the app

This is useful where we need large dependencies to build the app like in C++ or Rust project.

This will decrease image size to 39MB as compared to 56MB.

```
# It means we're copying from the first stage
COPY --from=0
```

```
docker build -t multi-node -f multi-node.Dockerfile .
docker run -p 3000:3000 multi-node
```
