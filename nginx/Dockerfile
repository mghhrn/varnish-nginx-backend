FROM nginx

RUN mkdir -p /home/nginx/logs

RUN apt-get update && apt-get install -y --no-install-recommends curl

COPY nginx/nginx.conf /etc/nginx/nginx.conf
COPY nginx/backendb.conf /etc/nginx/conf.d/backendb.conf

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /home/nginx/logs/access.log \
  && ln -sf /dev/stderr /home/nginx/logs/error.log

EXPOSE 80

CMD [ "nginx" ]
