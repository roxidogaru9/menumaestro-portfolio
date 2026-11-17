FROM maven:3.9.9-eclipse-temurin-21 AS api
WORKDIR /workspace/frontend
COPY frontend/pom.xml ./
COPY main-backend/endpoint/src/main/resources/ /workspace/main-backend/endpoint/src/main/resources/
RUN mvn -B generate-sources

FROM node:20-bookworm
WORKDIR /app
COPY frontend/package.json frontend/package-lock.json ./
RUN npm ci
COPY frontend/ ./
COPY --from=api /workspace/frontend/src/generated/ ./src/generated/
EXPOSE 4200
CMD ["node", "node_modules/@angular/cli/bin/ng.js", "serve", "--host", "0.0.0.0", "--port", "4200"]
