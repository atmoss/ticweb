FROM nginx:stable

RUN rm /etc/nginx/nginx.conf
COPY nginx.conf /etc/nginx/

ARG CERTBOT_EMAIL=contacto@ticsalud.cl
ARG DOMAIN_LIST=www.ticsalud.cl

RUN  apt-get update

RUN  apt-get install -y cron certbot python-certbot-nginx bash wget

RUN  certbot certonly --standalone --agree-tos -m "${CERTBOT_EMAIL}" -n -d ${DOMAIN_LIST}



VOLUME /etc/letsencrypt


CMD [ "sh", "-c", "cron && nginx -g 'daemon off;'" ]
