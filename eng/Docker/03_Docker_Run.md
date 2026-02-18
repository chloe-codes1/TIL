# What Happens When You Run a Docker Image?

### When executing the docker run command

- You can run a container from a locally stored Docker image
  - If the image does not exist on the system, it is pulled from an online registry

### image pull

- When an image is pulled, the `layers` are stored independently
- When running a container, these layers are `stacked` in order and `mounted` at a specific location
- By default, the layers belonging to the image are `read-only` and never change
- On top of them, a final `container-specific writable layer` is added, and all `changes` that occur in the container are saved to this layer

### Running a container

- When running a container, a clean layer is placed on top of the image's topmost layer
- No matter how many containers are running, they do not affect each other because the layer where actual `writes` occur is `separated`
  - In other words, every container has its own `unique writable area`, which becomes the topmost layer and does not affect any of the lower layers
