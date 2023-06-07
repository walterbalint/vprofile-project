# The first image is to build the artidact
FROM openjdk:11 AS BUILD_IMAGE

LABEL "Project"="vprofile"
LABEL "Author"="bwalter"

# Openjdk is based on debian
RUN apt update && apt install maven -y
RUN git clone https://github.com/walterbalint/vprofile-project.git
RUN cd vrpofile-project && git checkout docker && mvn install

# The second will be having the artifact
FROM tomcat:9-jre11
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE vrpofile-project/target/vrpofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
