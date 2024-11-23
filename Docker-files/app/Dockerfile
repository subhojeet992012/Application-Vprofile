FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone https://github.com/subhojeet992012/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn install

FROM tomcat:9-jre11

# Remove the default web applications and other unwanted files
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the application WAR file into the Tomcat webapps folder
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# Remove the default application.properties if it exists
RUN rm -f /usr/local/tomcat/webapps/ROOT/WEB-INF/classes/application.properties

# Copy the custom application.properties file from the current directory into the container
COPY application.properties /usr/local/tomcat/webapps/ROOT/WEB-INF/classes/application.properties

# Expose port 8080 to access the application
EXPOSE 8080

# Start Tomcat server
CMD ["catalina.sh", "run"]

