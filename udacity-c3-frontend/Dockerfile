## Build
FROM beevelop/ionic AS ionic
# Create app directory
WORKDIR /usr/src/app
# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

# fix bug npm WARN tarball tarball data for typescript@3.1.6 seems to be corrupted. Trying one more time.
RUN npm install -global typescript@3.1.6
RUN npm install -global @angular/cli

RUN npm ci
# Bundle app source
COPY . .
RUN ionic build

## Run 
FROM nginx:alpine
#COPY www /usr/share/nginx/html
COPY --from=ionic  /usr/src/app/www /usr/share/nginx/html

