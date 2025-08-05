# Docker Tags

> Reference: [docker docs](https://docs.docker.com/engine/reference/commandline/tag/)

<br>

<br>

## What are docker tags?

<br>

### Description

: You can manage versions of docker images using Docker tags

<br>

### Usage

: You can specify additional tags to existing images using Docker's `tag` command

```bash
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```

<br>

<br>

## What happens when you don't specify a tag?

<br>

### `latest` tag

- When creating Docker images, if `tag` name specification is omitted, the `latest` tag is attached as default value
- `latest` tag means the last **built / tagged** image without specifying a specific **tag / version**

<br>

### `latest` is Just a Tag, Doesn't Always Mean "Latest"

- `latest` doesn't actually mean the newest version

  - You might think **:latest** tag is always the most recently pushed image, but it's not
  - latest is just a tag given as default value for images without tags

- `latest` is not dynamic

  - If you don't attach a tag or don't specify the tag as **latest**, **:latest** is not affected or newly created

- For versioning, it's good practice not to use `latest` tag but to use **patch numbers** or **git commits** in tags 
