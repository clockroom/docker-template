FROM alpine:latest AS issue

WORKDIR /work

COPY ./ca.ext ./ca.ext

RUN apk --update add openssl \
  && openssl genrsa -out ca.key 2048 \
  && openssl req -new -key ca.key -subj "/CN=Private CA" -out ca.csr \
  && openssl x509 -req -in ca.csr -signkey ca.key -extfile ca.ext -days 3650 -out ca.crt

FROM scratch

WORKDIR /assets

COPY --from=issue /work/ca.key ./ca.key
COPY --from=issue /work/ca.crt ./ca.crt
