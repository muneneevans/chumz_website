# Stage 1 - development environment
# base image
FROM node:12.2.0-alpine as react-build
# set working directory
WORKDIR /app
# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# install and cache app dependencies
COPY package.json /app/package.json
COPY . .
RUN yarn
RUN yarn build


# Stage 2 - the production environment
FROM nginx:alpine
COPY nginx/chumz.conf /etc/nginx/conf.d/default.conf
COPY --from=react-build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]