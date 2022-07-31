# traefik

使用 [traefik](https://doc.traefik.io/traefik/)进行代理,[traefik](https://doc.traefik.io/traefik/)代理必须采用容器化



# 其他容器接入

```YAML
version: '3'
services:
   halo-server:
      image: halohub/halo
      container_name: halo
      #ports:
      #  - 8800:8090
      labels:
        - "traefik.enable=true"
        - "traefik.http.routers.halo-server.rule=Host(`blog.hb0730.me`)"
        - "traefik.http.routers.halo-server.entrypoints=http"
        - "traefik.http.routers.halo-server.service=halo-service"
        - "traefik.http.services.halo-service.loadbalancer.server.port=8090"
      environment:
        - VIRTUAL_PORT=8090
      volumes:
        - ./data:/root/.halo
      networks:
        - docker-net
networks:
   docker-net:
     external: true
```

核心请看`labels`





**注意**

不可不修改的copy,请注意异同点,相关参考[docs](https://doc.traefik.io/traefik/)