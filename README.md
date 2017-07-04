# Docker base images

## API viewer

Using Swagger UI https://github.com/swagger-api/swagger-ui.
Swagger UI app hosted by nginx.

Minimal docker compose configuration:

```yaml
api-viewer:
  image: sergef/docker-library-api-viewer:3.0.17
```

Point the stack proxy to the service:

```
server {
  listen 80;

  ...

  location /api/viewer {
    rewrite ^/api/viewer/?(.*)$ /$1 break;
    proxy_pass http://api-viewer;
  }

  ...
}
```

Enjoy url like this:
http://example.org/api/viewer/?url=http://example.org/api/v0/spec.

Where http://example.org/api/v0/spec
is the Open API specification (https://swagger.io/specification/).
