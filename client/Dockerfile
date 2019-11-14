FROM node:alpine as builder

#ENV http_proxy "http://proxy2:8080"
#ENV https_proxy "http://proxy2:8080"

#RUN npm config set http_proxy "http://proxy2:8080"
#RUN npm config set https_proxy "http://proxy2:8080"

#RUN npm config get http_proxy
#RUN npm config get https-proxy


WORKDIR '/app'
COPY ./package.json ./

RUN npm cache clean --force
RUN npm install
COPY . .
RUN npm run build

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html