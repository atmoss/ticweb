FROM nginx:1.21.0

RUN rm /etc/nginx/nginx.conf
COPY nginx.conf /etc/nginx/

ARG CERTBOT_EMAIL=contacto@ticsalud.cl
ARG DOMAIN_LIST=www.ticsalud.cl

RUN  apt-get update

RUN  apt-get install -y cron certbot python-certbot-nginx bash wget

RUN  certbot certonly --standalone --agree-tos -m "${CERTBOT_EMAIL}" -n -d ${DOMAIN_LIST}

RUN  rm -rf /var/lib/apt/lists/*

RUN  echo "PATH=$PATH" > /etc/cron.d/certbot-renew

RUN  echo "@monthly certbot renew --nginx >> /var/log/cron.log 2>&1" >> /etc/cron.d/certbot-renew

RUN  crontab /etc/cron.d/certbot-renew



VOLUME /etc/letsencrypt


CMD [ "sh", "-c", "cron && nginx -g 'daemon off;'" ]
