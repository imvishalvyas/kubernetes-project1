# backend/Dockerfile
FROM openjdk:8-jdk-alpine

# Set working directory
WORKDIR /app

# Clone the repo (or COPY if you already have code locally)
RUN apk add --no-cache git maven \
    && git clone https://github.com/shephertz/App42PaaS-Java-PostgreSQL-Sample.git . \
    && mvn clean package -DskipTests

# Expose backend port
EXPOSE 8080

# Run the app (adjust JAR path if needed)
CMD ["java", "-jar", "target/App42PaaS-Java-PostgreSQL-Sample-0.1-SNAPSHOT.jar"]