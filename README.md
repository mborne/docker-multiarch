# docker-multiarch

Experimentation to build multi-arch image for docker.

## Usage

* Install qemu

```bash
sudo apt-get update
sudo apt-get install -y qemu-user-static
sudo apt-get install -y binfmt-support
# alternative :
# sudo docker run --rm --privileged multiarch/qemu-user-static --reset -p yes
```

* Setup buildx :

```bash
docker buildx create --name builder
docker buildx use builder
docker buildx inspect --bootstrap
docker buildx ls
```

* Build images :

```bash
docker buildx build --push \
    --platform linux/arm/v7,linux/arm64/v8,linux/amd64 \
    --tag registry.quadtreeworld.net/multiarch:latest .
```

## Ressources

* [medium.com - @artur.klauser - Building Multi-Architecture Docker Images With Buildx](https://medium.com/@artur.klauser/building-multi-architecture-docker-images-with-buildx-27d80f7e2408)
