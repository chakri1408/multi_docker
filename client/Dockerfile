FROM node:16-alpine AS builder
WORKDIR /app
COPY ./package.json ./package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build


FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf 
# we copied the default.conf file to the nginx conf.d directory
# so that nginx can use it as its configuration file as the upstream port
# is 3000 we added it in nginx configuration file and also we exposed the 
# port 3000 in the dockerfile so that we can access the application from outside the container
COPY --from=builder /app/build /usr/share/nginx/html