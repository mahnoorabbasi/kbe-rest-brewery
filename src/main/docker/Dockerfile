FROM openjdk:11-jre-slim as builder
WORKDIR application
COPY maven/${project.build.finalName}.jar ./
#COPY maven/kbe-rest-brewery-0.0.1-SNAPSHOT.jar ./
#maven property avail at rutime which is project name
RUN java -Djarmode=layertools -jar ${project.build.finalName}.jar extract

#RUN java -Djarmode=layertools -jar kbe-rest-brewery-0.0.1-SNAPSHOT.jar extract

FROM openjdk:11-jre-slim
WORKDIR application
COPY --from=builder application/dependencies/ ./
COPY --from=builder application/spring-boot-loader/ ./
COPY --from=builder application/snapshot-dependencies/ ./
COPY --from=builder application/application/ ./
ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "org.springframework.boot.loader.JarLauncher"]