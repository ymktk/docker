FROM  gradle:5.6.4-jdk8 AS builder
WORKDIR /app

COPY ./demo/gradle          ./gradle
COPY ./demo/src             ./src
COPY ./demo/build.gradle    ./
COPY ./demo/gradlew         ./
COPY ./demo/settings.gradle ./

RUN  ./gradlew build

################################################################################
From openjdk:8-jre-alpine3.9 AS release

COPY --from=builder /app/build/libs/demo-0.0.1-SNAPSHOT.jar /app.jar

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]

EXPOSE 8085
