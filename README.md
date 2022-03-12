# nlp-notebook
This is a Docker integrated environment for natural language processing

## How to use
### Initial build for Docker image
To begin with, you have to build a Docker image by `build` command.
```bash
docker-compse build
```

### Start up Docker containers
Let's start up docker containers by `up` command in background `-d`.
```bash
docker-compse up -d
```

To build images before starting containers, use `--build` option.
```
docker-compse up -d --build
```

### Use an interactive shell in container
To run `bash` in the running container and connect it, use `exec` command.
```
docker-compse exec <container_name> /bin/bash
```