FROM node:alpine As development

WORKDIR /usr/src/app

COPY package.json /.
COPY yarn.lock /.

RUN yarn install

COPY . .

RUN yarn build

FROM node:alpine As production

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

WORKDIR /usr/src/app

COPY package.json /.
COPY yarn.lock /.

RUN npm install -g yarn

RUN yarn install --production=true

COPY --from=development /usr/app/src/dist ./dist

CMD ["node", "dist/apps/reservations/main"]