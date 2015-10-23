
## Anthracite Dockerfile

A supervisord controlled Anthracite Event Manager running in Debian 7. 

Info: https://github.com/Dieterbe/anthracite/

Usage:
```
docker run --restart=always \
           --name=anthracite \
           -e ANTHRACITE_TZ=America/Halifax \ 
           -e ES_URL=http://elasticsearch:9200 \
           -e ES_INDEX=anthracite-es \
           -p 8081:8081 \
           -d v00rh33s/anthracite
```

Ports:
 8081 - WebInterface / REST API

## Docker Compose
Quick docker-compose example (elasticsearch config out of scope but note ES_INDEX): 

```
elasticsearch:
  build: elasticsearch/
  container_name: elasticsearch
  ports:
    - "9200:9200"
    - "9300:9300"
  volumes:
    - ./elasticsearch/config/:/elasticsearch/config/
    - /data/anthracite/storage/:/usr/share/elasticsearch/data
  command: elasticsearch -Des.node.name='anthracite-es'

anthracite:
  image: v00rh33s/anthracite
  container_name: anthracite
  environment:
    - ANTHRACITE_TZ=Amercia/Halifax
    - ES_URL=http://elasticsearch:9200
    - ES_INDEX=anthracite-es
  ports:
    - "8081:8081"
  links:
    - elasticsearch
```