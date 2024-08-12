FROM node:alpine As development

WORKDIR /usr/src/app

COPY package.json yarn.lock ./
COPY tsconfig.json tsconfig.json

RUN yarn install

COPY apps/auth apps/auth
COPY libs libs

RUN yarn build

FROM node:alpine As production

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

WORKDIR /usr/src/app

COPY package.json yarn.lock ./

RUN yarn install --production=true

COPY --from=development /usr/src/app/dist ./dist

CMD ["node", "dist/apps/auth/main"]
