FROM docker.io/nginx:alpine
LABEL org.opencontainers.image.source = "https://github.com/mcsps/docker-images"

# source: https://github.com/nginxinc/docker-nginx-unprivileged/

# Add System Tools
RUN apk add --update --no-cache bash curl wget git busybox-extras mysql-client && apk upgrade
# implement changes required to run NGINX as an unprivileged user
RUN sed -i -e '/listen/!b' -e '/80;/!b' -e 's/80;/8080;/' /etc/nginx/conf.d/default.conf \
    && sed -i -e '/    index  index.html index.htm;/a \ \ \ \     autoindex on;' /etc/nginx/conf.d/default.conf \
    && sed -i -e '/user/!b' -e '/nginx/!b' -e '/nginx/d' /etc/nginx/nginx.conf \
    && sed -i 's!/var/run/nginx.pid!/tmp/nginx.pid!g' /etc/nginx/nginx.conf \
    && sed -i '/http {/a \
    set_real_ip_from 0.0.0.0/0;\
    real_ip_header X-Forwarded-For;\
    real_ip_recursive on;' /etc/nginx/nginx.conf \
    && sed -i "/^http {/a \    proxy_temp_path /tmp/proxy_temp;\n    client_body_temp_path /tmp/client_temp;\n    fastcgi_temp_path /tmp/fastcgi_temp;\n    uwsgi_temp_path /tmp/uwsgi_temp;\n    scgi_temp_path /tmp/scgi_temp;\n" /etc/nginx/nginx.conf


# nginx user must own the cache directory to write cache
RUN chown -R 101:0 /var/cache/nginx \
	&& chmod -R g+w /var/cache/nginx

# create *_temp folders and set permissions
RUN mkdir -p /tmp/proxy_temp \
   && chown -R 101:0 /tmp/proxy_temp \
   && chmod -R g+w /tmp/proxy_temp \
   && mkdir -p /tmp/client_temp \
   && chown -R 101:0 /tmp/client_temp \
   && chmod -R g+w /tmp/client_temp \
   && mkdir -p /tmp/fastcgi_temp \
   && chown -R 101:0 /tmp/fastcgi_temp \
   && chmod -R g+w /tmp/fastcgi_temp \
   && mkdir -p /tmp/uwsgi_temp \
   && chown -R 101:0 /tmp/uwsgi_temp \
   && chmod -R g+w /tmp/uwsgi_temp \
   && mkdir -p /tmp/scgi_temp \
   && chown -R 101:0 /tmp/scgi_temp \
   && chmod -R g+w /tmp/scgi_temp

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 8080

USER 101:101
