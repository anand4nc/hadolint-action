FROM node:16-alpine as BUILDER
WORKDIR /usr/app

COPY ./dist/apps/bjs-fe/package.json ./
RUN --mount=type=cache,target=~/.yarn_cache YARN_CACHE_FOLDER=~/.yarn_cache yarn install --frozen-lockfile

FROM node:16-alpine
RUN adduser -D -g '' appuser
COPY ./dist/apps/bjs-fe/ /usr/src/app
WORKDIR /usr/src/app
COPY --from=BUILDER /usr/app/node_modules ./node_modules
USER appuser
EXPOSE 3000
CMD ["yarn", "start"]
