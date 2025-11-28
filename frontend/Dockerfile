
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .

RUN npm run build -- --configuration production


FROM nginx:alpine

COPY --from=build /app/dist /usr/share/nginx/html

RUN sed -i 's/listen       80;/listen       8081;/' /etc/nginx/conf.d/default.conf
EXPOSE 8081
CMD ["nginx", "-g", "daemon off;"]
