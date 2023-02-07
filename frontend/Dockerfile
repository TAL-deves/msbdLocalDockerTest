# pull the Node.js Docker image
FROM node:alpine as builder

# create the directory inside the container
WORKDIR ./frontend

# copy the package.json files from local machine to the workdir in container
COPY package*.json ./

# run npm install in our local machine
RUN npm install --force

# copy the generated modules and all other files to the container
COPY . ./

# the command that starts our app
RUN npm run build

#stage 2

FROM nginx

# WORKDIR /usr/share/nginx/html
COPY default.conf /etc/nginx/conf.d/default.conf
# COPY fullchain.pem /etc/nginx/conf.d/fullchain.pem
# COPY privkey.pem /etc/nginx/conf.d/privkey.pem

# Copies static resources from builder stage  --from=builder
COPY --from=builder ./frontend/build /var/www/html

EXPOSE 80
# EXPOSE 443
# EXPOSE 90
# EXPOSE 445

RUN chown nginx.nginx /var/www/html/ -R
# Containers run nginx with global directives and daemon off

# ENTRYPOINT ["nginx", "-g", "daemon off;"]