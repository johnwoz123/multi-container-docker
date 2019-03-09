FROM node:11.10-alpine as builder
WORKDIR '/app'
COPY package.json .
RUN npm install
COPY . .
RUN npm run build

# /app/build <-- all we care about

FROM nginx
#elastic beanstalk will use this exposed port
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# copy from the builder phase above - from directory - to directory
COPY --from=builder /app/build /usr/share/nginx/html