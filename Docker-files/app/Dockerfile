FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone https://github.com/davidlimacardoso/devops-vprofile-project.git
RUN cd devops-vprofile-project\
    && git checkout containers\
    && mvn install


FROM tomcat:9-jre11
LABEL Project="vprofile"
LABEL Key="David Cardoso"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE devops-vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war
EXPOSE 8080
CMD [ "catalina.sh", "run" ]