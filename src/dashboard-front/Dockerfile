# npm part
FROM node:20.19.4-bookworm AS builder

WORKDIR /app
COPY . /app

ENV NODE_OPTIONS=--max_old_space_size=8192

RUN npm install -g npm@11.5.2
RUN npm install --force
RUN npm run build-only

# nginx part
FROM tencentos/tencentos4-minimal 

RUN dnf -y install nginx && \
    dnf clean all && \
    ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log

# cp nginx files
COPY custom-configs/default /etc/nginx/conf.d/default.conf
# COPY custom-configs/30-render /etc/cont-init.d/30-render
COPY --from=builder /app/dist/ /var/www/
