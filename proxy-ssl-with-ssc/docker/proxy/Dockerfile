FROM proxy-ssl-with-ssc-issue:latest as issue

FROM alpine:latest AS server_issue

WORKDIR /work

COPY --from=issue /assets/ca.key ./ca.key
COPY --from=issue /assets/ca.crt ./ca.crt
COPY ./server.ext ./server.ext

RUN apk --update add openssl \
  && openssl genrsa -out server.key 2048 \
  && openssl req -new -key server.key -subj "/CN=localhost" -out server.csr \
  && openssl x509 -req -in server.csr -CA ca.crt -CAkey ca.key -extfile server.ext -days 365 -out server.crt

FROM nginx:1-alpine-slim

COPY --from=issue /assets/ca.crt /etc/nginx/ssl/ca.crt
COPY --from=server_issue /work/server.key /etc/nginx/ssl/server.key
COPY --from=server_issue /work/server.crt /etc/nginx/ssl/server.crt
RUN chmod 400 /etc/nginx/ssl/server.key

COPY ./default.conf /etc/nginx/conf.d/default.conf

EXPOSE 443
