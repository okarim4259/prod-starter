FROM node:alpine as builder
WORKDIR '/app'
COPY . /app
RUN npm config set proxy http://proxyprod.com:8001
RUN npm install -g @angular/cli
RUN npm install -g @angular/cli
RUN npm install
RUN npm run build -- --prod --output-path=dist

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
RUN rm -rf /usr/share/nginx/html/*
COPY --from=builder /app/dist /usr/share/nginx/html