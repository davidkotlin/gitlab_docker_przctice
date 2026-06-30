FROM ubuntu:22.04
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y nginx && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

COPY gitlab_nginx /etc/nginx/sites-available/gitlab_nginx

RUN ln -sf /etc/nginx/sites-available/gitlab_nginx /etc/nginx/sites-enabled/gitlab_nginx && \
    rm -f /etc/nginx/sites-enabled/default

CMD ["nginx", "-g", "daemon off;"]
