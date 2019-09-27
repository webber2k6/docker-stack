FROM nginx:alpine

RUN apk add --no-cache bash gawk sed grep bc coreutils \
 && rm -rf /var/cache/apk/*

RUN mkdir /etc/nginx/conf.d/custom \
 && mkdir /etc/nginx/conf.d/partials

COPY defaults/nginx.conf /etc/nginx/nginx.conf
COPY defaults/fastcgi_params /etc/nginx/fastcgi_params
COPY defaults/overall_params.conf /etc/nginx/overall_params.conf
COPY defaults/partials/* /etc/nginx/conf.d/partials/
COPY defaults/php.conf /etc/nginx/conf.d/default.conf

CMD ["nginx", "-g", "daemon off;"]