FROM ubuntu:jammy
RUN apt-get update
RUN apt-get install vim wget apt-transport-https lsb-release ca-certificates gnupg -y

RUN mkdir -p /etc/ssl/nginx
COPY nginx-repo.crt /etc/ssl/nginx/
COPY nginx-repo.key /etc/ssl/nginx/
RUN chmod 755 /etc/ssl/nginx/nginx-repo.crt
RUN chmod 755 /etc/ssl/nginx/nginx-repo.key
COPY nginx-plus.list /etc/apt/sources.list.d/

RUN wget -q -O /var/tmp/nginx_signing.key https://cs.nginx.com/static/keys/nginx_signing.key && apt-key add /var/tmp/nginx_signing.key
RUN wget -q -O /etc/apt/apt.conf.d/90pkgs-nginx https://cs.nginx.com/static/files/90pkgs-nginx

RUN apt-get update
RUN apt-get install nginx-plus nginx-plus-module-njs -y

RUN ln -sf /dev/stdout /var/log/nginx/access.log && ln -sf /dev/stderr /var/log/nginx/error.log
CMD ["nginx", "-g", "daemon off;"]
