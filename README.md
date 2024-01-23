# DockerPlayground

## Docker Basic

### Run an interactive shell in the container

```sh
docker run -it [ImageName] sh
```

### Why change the dev scripts?

Without the host flag, the app can only be accessed inside the container, not from host (machine's web browser),
So Change from

```json
"scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "lint": "eslint . --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview"
  },
```

to

```json
"scripts": {
    "dev": "vite --host",
    "build": "tsc && vite build",
    "lint": "eslint . --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview"
  },
```

### Dev enviroument with docker?

```sh
docker run -p [port]:[port] -v "$(pwd):/app" -v /app/node_modules [imageName]
```

- -p [port]:[port]
  The -p option is used for port mapping. It maps a port on your host machine to a port in the Docker container.
- -v "$(pwd):/app"

  The -v option is used to mount volumes.
  $(pwd) is a shell command that gets replaced by your current working directory on the host machine. This directory is being mounted to /app in the container.
  This means that the contents of your current directory on your host machine are directly accessible in /app inside the container. This is often done for development purposes to allow for live code updates without needing to rebuild the image.

- -v /app/node_modules
  This is to ensure that the node_modules directory inside the container (which may have platform-specific builds) is not overwritten by the host's node_modules directory due to the previous volume mount. Essentially, it preserves the node_modules directory as created within the container.

### Push to Docker Hub

Similar to the GitHub

1. Tag the local image with the remote repository

```sh
docker tag [local-image]:[tag] [your-username]/[repository-name]:[tag]
```

2. Push the image to the Docker Hub(default is public)

```sh
docker push [your-username]/[repository-name]:[tag]
```

## Docker Compose
