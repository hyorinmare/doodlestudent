FROM node:16-alpine AS build

ARG DEBIAN_FRONTEND=noninteractive

ENV NG_CLI_ANALYTICS=ci
RUN apk update && apk upgrade &&\
    apk add --no-cache bash git

RUN git clone https://github.com/hyorinmare/doodlestudent.git /app --depth=1

WORKDIR /app/front

RUN npm install --force

RUN npm run build --prod

FROM nginx:stable-alpine AS prod
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/front/dist/tlcfront /usr/share/nginx/html

EXPOSE 8080

RUN mkdir /etc/letsencrypt && chown root:101 /etc/letsencrypt && chmod 770 /etc/letsencrypt
