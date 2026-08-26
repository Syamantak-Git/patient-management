FROM maven:3.9.16-eclipse-temurin-25-noble AS builder

WORKDIR /app

COPY pom.xml .

RUN mvn dependency:go-offline -B

COPY src ./src

RUN mvn clean package -DskipTests

FROM eclipse-temurin:25-jre-alpine AS runner

WORKDIR /app

COPY --from=builder /app/target/billing-service-0.0.1-SNAPSHOT.jar ./app.jar

EXPOSE 4001
EXPOSE 9001

ENTRYPOINT [ "java", "-jar", "app.jar" ]