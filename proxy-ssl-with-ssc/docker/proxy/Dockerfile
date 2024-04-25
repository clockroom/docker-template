FROM alpine:latest as ssl

WORKDIR /work

COPY ./san.txt /work/san.txt

RUN apk --update add openssl \
  && openssl genrsa -out client.key 2048 \
  && openssl req -new -key client.key -subj "/CN=localhost ca" -out client.csr \
  && openssl x509 -in client.csr -days 3650 -req -signkey client.key -out client.crt \
  && openssl genrsa 2048 > server.key \
  && openssl req -new -key server.key -subj "/CN=localhost" -out server.csr \
  && openssl x509 -in server.csr -days 3650 -req -CA client.crt -CAkey client.key -CAcreateserial -extfile san.txt -out server.crt

FROM nginx:1.25-alpine-slim

EXPOSE 443

COPY --from=ssl /work/client.crt /etc/nginx/ssl/client.crt
COPY --from=ssl /work/server.key /etc/nginx/ssl/server.key
COPY --from=ssl /work/server.crt /etc/nginx/ssl/server.crt
RUN chmod 400 /etc/nginx/ssl/server.key

COPY ./default.conf /etc/nginx/conf.d/default.conf
