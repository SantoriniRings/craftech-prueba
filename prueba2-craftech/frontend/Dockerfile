#Build Stage React

FROM node:18 AS builder
WORKDIR /app-front
COPY package.json package-lock.json ./
RUN npm install
COPY . .
RUN npm run build

#Production Stage React
FROM nginx:alpine
COPY --from=builder /app-front/build usr/share/nginx/html
COPY nginx/default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

