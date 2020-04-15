# builder
FROM openjdk:8 as builder

# update and install dependancies
RUN apt-get -y update && apt-get -y install maven

# copy assets
WORKDIR /build
COPY . ./

# build the target WAR file
RUN cd fcrepo-webapp/fcrepo-webapp-saxon && mvn clean package

# base image
FROM tomcat:8.0

# install updates and dependancies
RUN apt-get -y update && apt-get -y install

# add the healthcheck
RUN mkdir /usr/local/tomcat/webapps/healthcheck && echo "OK" > /usr/local/tomcat/webapps/healthcheck/index.html

# port and run command
EXPOSE 8080

# copy the WAR file
COPY --from=builder /build/fcrepo-webapp/fcrepo-webapp-saxon/target/saxon.war /usr/local/tomcat/webapps/

#
# end of file
#
