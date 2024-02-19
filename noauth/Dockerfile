# Stage 1
FROM node:18-alpine as builder
RUN apk add git bash
RUN git clone https://github.com/nostrband/noauth.git
WORKDIR /noauth
RUN npm install
ARG REACT_APP_WEB_PUSH_PUBKEY
ENV REACT_APP_WEB_PUSH_PUBKEY=$REACT_APP_WEB_PUSH_PUBKEY
ARG REACT_APP_NOAUTHD_URL
ENV REACT_APP_NOAUTHD_URL=$REACT_APP_NOAUTHD_URL
ARG REACT_APP_DOMAIN
ENV REACT_APP_DOMAIN=$REACT_APP_DOMAIN
ARG REACT_APP_RELAY
ENV REACT_APP_RELAY=$REACT_APP_RELAY
RUN npm run build
FROM node:18-alpine
RUN apk add git bash busybox-extras
RUN npm install serve -g --silent
WORKDIR /app
COPY --from=builder /noauth/build .
EXPOSE 3210
CMD ["serve", "-p", "3210", "-s", "."]doc
