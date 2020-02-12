- Linux containers require the Docker host to be running a Linux kernel.
  - For example, Linux containers cannot run directly on Windows Docker hosts.
  - The same is true of Windows containers - they need to run on a Docker host with a Windows kernel
  - Figure out this is why? Because that means docker isn't that platform-independent?

- You can commit a container to make an image from it
  - but you should avoid that wherever possible.
  - It’s much better to use a repeatable Dockerfile to build your image.

- Network traffic cannot reach containers from the host unless ports are explicitly published.

- build from the current Dockerfile:
  -  docker image build --tag $DOCKERID/linux_tweet_app:1.0 .

- run the container

```
docker container run \
--detach \
--publish 80:80 \
--name linux_tweet_app \
$DOCKERID/linux_tweet_app:1.0
```

- run with a bind mount

```
docker container run \
--detach \
--publish 80:80 \
--name linux_tweet_app \
--mount type=bind,source="$(pwd)",target=/usr/share/nginx/html \
$DOCKERID/linux_tweet_app:1.0
```

- Notice that several lines of the output say 'Layer already exists'.
  - This is because Docker will leverage read-only layers that are the same as any previously uploaded image layers.
