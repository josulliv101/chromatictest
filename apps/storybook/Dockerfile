# For running @chromatictest/storybook in Docker container.

# Build Storybook to static files
FROM node:16-alpine3.11 AS builder
WORKDIR /app
COPY package.json yarn.lock babel.config.js ./
COPY apps/storybook ./apps/storybook
COPY packages ./packages
RUN yarn install --frozen-lockfile
RUN yarn build
RUN yarn workspace @chromatictest/storybook run build-storybook

# Run built static files
FROM nginx:alpine
WORKDIR /usr/share/nginx/html
COPY apps/storybook/nginx.conf /etc/nginx/nginx.conf
COPY --from=builder /app/apps/storybook/storybook-static .
