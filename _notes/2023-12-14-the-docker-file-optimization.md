---
layout: post
usehighlight: false
tags: [platform-infrastructure, optimization,docker]
title: The docker file optimization
---
## Stage 1: Build Stage

**Efficient Caching:** By copying only the necessary files for installing dependencies and running the build process in this stage, Docker can cache these layers. If the `package.json` and `package-lock.json` files do not change, Docker will use the cached layer for the `npm install` step. This speeds up the build process by avoiding unnecessary reinstallation of dependencies when the application code hasn't changed.

**Reduced Image Size:** The build process typically involves installing development dependencies and building artifacts. By performing the build in a separate stage, you ensure that only the necessary artifacts (in the build directory) and production dependencies are carried over to the final image. This reduces the size of the final Docker image.

## Stage 2: Production Image Stage

**Smaller Final Image:** The second stage only copies over the minimal set of files needed for the production runtime. This results in a smaller and more lightweight production image.

**Security and Least Privilege:** The final production image only includes the built application (`/app/dist`) and production dependencies. By excluding unnecessary files and development dependencies, you follow the principle of least privilege and reduce the potential attack surface of your production environment.

**Clear Separation of Concerns:** Separating the build stage from the production image stage provides a clear distinction between the development/build environment and the production runtime environment. This separation helps improve maintainability and ensures that development-specific tools or dependencies do not end up in the production image.

```dockerfile
### Stage 1: Build the Node.js app

FROM node:18-alpine as build

WORKDIR /app

# Copy only package.json and package-lock.json to leverage Docker cache

COPY package.json .
COPY package-lock.json .
COPY tsconfig.json .

# --production skips the installation of packages listed in the "devDependencies" section of your package.json.

RUN npm install --production

COPY . .
RUN npm run build

# Stage 2: Create a lightweight production image

FROM node:18-alpine

WORKDIR /app

# Copy only necessary files from the build stage

COPY --from=build /app/dist ./dist
COPY --from=build /app/node_modules ./node_modules
COPY --from=build /app/package*.json ./
COPY --from=build /app/tsconfig.json ./

EXPOSE 80

CMD ["node", "dist/index.js"]
``````

**NOTE:** `--production` is added just for information. You should not use it in typescript projects because typescript is development dependency and you need it during build process.