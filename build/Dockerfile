
FROM node:10.15.3 as build-deps-wizard
ARG VERSION

RUN echo $VERSION

# # build wizard
# WORKDIR /usr/src/app/wizard
# COPY wizard .
# RUN yarn
# RUN rm -Rf build && yarn run build

# # build monitor
# WORKDIR /usr/src/app/monitor
# COPY monitor .
# RUN npm i --production

# build final image
FROM node:current-alpine3.12

WORKDIR /usr/src/app
USER root

RUN apk add -U --no-cache supervisor

# COPY --from=build-deps-wizard /usr/src/app/monitor /usr/src/monitor
# COPY --from=build-deps-wizard /usr/src/app/wizard/build /usr/src/monitor/wizard

COPY files/supervisord.conf /etc/supervisord/

ENTRYPOINT supervisord -n -c /etc/supervisord/supervisord.conf
