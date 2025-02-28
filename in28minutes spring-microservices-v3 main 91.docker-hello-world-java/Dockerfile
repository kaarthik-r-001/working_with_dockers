# Build stage
FROM jelastic/maven:3.9.5-openjdk-21 AS buildd
WORKDIR /kaarthik
COPY . /kaarthik
RUN mvn -f /kaarthik/pom.xml clean package

# Find the jar file in the build stage
RUN find /kaarthik -name "*.jar" -exec cp {} /kaarthik/app.jar \;

# Runtime stage
FROM openjdk:21-jdk-slim
EXPOSE 5000

# Copy the found jar file
COPY --from=buildd /kaarthik/app.jar /app.jar

# Run the application
ENTRYPOINT ["sh", "-c", "java -jar /app.jar"]
