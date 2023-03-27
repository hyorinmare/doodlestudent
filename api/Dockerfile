FROM eclipse-temurin:17-alpine as build
LABEL stage=build
RUN apk --no-cache add git
RUN git clone https://github.com/hyorinmare/doodlestudent.git /app --depth=1
WORKDIR /app/api
RUN chmod +x mvnw
RUN ./mvnw clean package -Dquarkus.package.type=uber-jar

FROM eclipse-temurin:17-jre-ubi9-minimal as quarkus_app
WORKDIR /app
COPY --from=build /app/api/target/tlcdemoApp-1.0.0-SNAPSHOT-runner.jar ./application.jar
EXPOSE 8080
CMD ["java", "-jar", "/app/application.jar"]
