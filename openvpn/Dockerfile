FROM alpine:3.8

COPY start.sh /start.sh
RUN apk add --update --no-cache curl
RUN apk add --update --no-cache openvpn
RUN apk add --no-cache bash
ENTRYPOINT ["/start.sh"]