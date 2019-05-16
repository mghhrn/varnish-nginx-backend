# docker-varnish-nginx-example
Simple example of using `docker-compose` to configure nginx behind varnish 

### Usage
From the repo root, run:

```bash
docker-compose -p example up
```

The first time you run this, docker will need to download several images used by the services defined in [docker-compose.yml](https://github.com/montmanu/docker-varnish-nginx-example/blob/master/docker-compose.yml).
Each service's image is built using it's respective `Dockerfile` (e.g., [nginx/Dockerfile](https://github.com/montmanu/docker-varnish-nginx-example/blob/master/nginx/Dockerfile)).  


### Attention
You must put your jar file in the same directory as where docker-compose.yml exists. 
