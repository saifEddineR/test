FROM node:18.13.0-alpine3.17 as build-stage
WORKDIR /app

COPY [ "package.json" , "./"]

RUN npm i

COPY . .

RUN npm run build

#1.	Running our build_app on Nginx server-----------------------------------------------------------------------

FROM nginx:stable-alpine as production-stage

COPY  --from=build-stage /app/public /usr/share/nginx/html/
COPY --from=build-stage /app/build /usr/share/nginx/html/

COPY nginx/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
