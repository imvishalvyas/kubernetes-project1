# Start from Tomcat with JDK 8
FROM tomcat:9.0-jdk8-temurin

# Install git and maven to build the app
RUN apt-get update && apt-get install -y git maven && rm -rf /var/lib/apt/lists/*

WORKDIR /build

# Clone the project and build a WAR file
RUN git clone https://github.com/shephertz/App42PaaS-Java-PostgreSQL-Sample.git . \
    && mvn clean package -DskipTests

# Remove default apps and deploy our WAR
RUN rm -rf /usr/local/tomcat/webapps/* \
    && cp target/*.war /usr/local/tomcat/webapps/ROOT.war

# Expose Tomcat default port
EXPOSE 8080

# Launch Tomcat
CMD ["catalina.sh", "run"]
