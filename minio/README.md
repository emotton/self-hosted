# nginx proxy manager

```
version: '3.8'

services:
  minio:
    image: quay.io/minio/minio
    command: server /data --console-address ":9001"
    container_name: minio
    ports:
      - "9000:9000"
      - "9001:9001"
    environment:
      MINIO_ROOT_USER: administrador
      MINIO_ROOT_PASSWORD: senha
      MINIO_BROWSER_REDIRECT_URL: https://console.seudominio.com
      MINIO_SERVER_URL: https://s3.seudominio.com
    volumes:
      - minio_data:/data
    networks:
      - npm_public
    deploy:
      mode: replicated
      replicas: 1
      placement:
        constraints:
          - node.role == manager
      resources:
        limits:
          memory: 4G

volumes:
  minio_data:
    external: true

networks:
  npm_public:
    external: true
```	
	
```	
docker-compose up -d
```

