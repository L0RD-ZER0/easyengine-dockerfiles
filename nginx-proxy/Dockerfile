FROM jwilder/nginx-proxy:1.5.2
LABEL org.label-schema.schema-version="1.0.0"
LABEL org.label-schema.vendor="EasyEngine"
LABEL org.label-schema.name="nginx-proxy"

COPY nginx.tmpl /app/
COPY nginx.conf /etc/nginx/nginx.conf
COPY version.conf /version.conf

RUN apt-get update \
    && apt-get install --no-install-recommends apache2-utils -y && rm -rf /var/lib/apt/lists/*

# add updated docker-gen or it errors real bad, and I mean real bad
RUN mkdir /dg && \
    curl -L 'https://github.com/nginx-proxy/docker-gen/releases/download/0.14.0/docker-gen-linux-amd64-0.14.0.tar.gz' | \
    tar xvzf - -C '/dg' && \
    chmod +x /dg/docker-gen && \
    mv /dg/docker-gen /usr/local/bin/docker-gen && \
    rm -rf /dg

RUN chmod +x /app/docker-entrypoint.sh
RUN rm -rf /var/log/nginx/access.log /var/log/nginx/error.log && touch /var/log/nginx/access.log /var/log/nginx/error.log
