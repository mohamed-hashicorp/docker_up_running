# Docker up & running - Chapter 4

- to build an image
```
$ cd docker-node-hello
$ docker image build -t example/docker-node-hello:latest .
```

- to run an image
```
$ docker container run --rm -d -p 8080:8080 example/docker-node-hello:latest
```

- confirm container is running
```
$ docker ps
CONTAINER ID   IMAGE                              COMMAND                  CREATED        STATUS        PORTS                                         NAMES
763aabdb1b9e   example/docker-node-hello:latest   "docker-entrypoint.s…"   23 hours ago   Up 23 hours   0.0.0.0:8080->8080/tcp, [::]:8080->8080/tcp   nice_swirles
```

- access the container
```
$ curl http://localhost:8080
Hello World. Wish you were here.
```

- stop a container
```
$ docker container stop 763aabdb1b9e
763aabdb1b9e
```

- modify container arguments
```
$ docker container run --rm -d \
    --publish mode=ingress,published=8080,target=8080 \
    --env WHO="Sean and Karl" \
    example/docker-node-hello:latest
baaa6bc8e36b334da08e03c48edf50938f9303de5846e112deb6db5d69a08231
$ curl http://127.0.0.1:8080
Hello Sean and Karl. Wish you were here.
```

- Store an image to a public registries
```
$ docker login
Login with your Docker ID to push and pull images from Docker Hub. If you
don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: <hub_username>
Password: <hub_password/token>
Login Succeeded

Logging in with your password grants your terminal complete access to
your account.
$ docker image tag example/docker-node-hello:latest \
docker.io/<hub_username>/docker-node-hello:latest
$ docker push docker.io/<hub_username>/docker-node-hello:latest
```

- 
