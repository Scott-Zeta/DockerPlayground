# DockerPlayground

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
