dependencies: 
- docker
- jdk 8
- nexus
- gradle
- rabbitmq
- sujiakeji-eureka-server
- sujiakeji-config-server

update dependencies:
```
gradle dependencyUpdates -Drevision=release --info
```

build: 
```
cd sujiakeji-zuul
./gradlew idea
./gradlew clean build copyJar -x test
```

start:
```
java -Dspring.profiles.active=dev \
  -DEUREKA_SERVER_HOST=localhost \
  -DEUREKA_SERVER_PORT=9000 \
  -DRABBITMQ_HOST=localhost \
  -DRABBITMQ_PORT=5672 \
  -jar build/libs/sujiakeji-zuul.jar
```

docker:
```
./gradlew docker

docker build -t sujiakeji/sujiakeji-zuul:1.0.0-SNAPSHOT .

docker run -it --rm \
  --name sujiakeji-zuul \
  -p 9300:9300 \
  --link sujiakeji-eureka-server \
  --link sujiakeji-rabbitmq \
  -e EUREKA_SERVER_HOST=sujiakeji-eureka-server \
  -e EUREKA_SERVER_PORT=9000 \
  -e RABBITMQ_HOST=sujiakeji-rabbitmq \
  -e RABBITMQ_PORT=5672 \
  -e SPRING_PROFILES_ACTIVE=dev \
  sujiakeji/sujiakeji-zuul

docker-compose up
```
