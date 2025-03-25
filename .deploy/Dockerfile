# build stage
FROM node:22-alpine as build
WORKDIR /app
COPY package*.json ./
RUN corepack enable

RUN yarn 
COPY . .
RUN yarn build

# production stage
FROM nginx:stable as production
COPY --from=build /app/dist /usr/share/nginx/html
COPY ./deploy/nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]