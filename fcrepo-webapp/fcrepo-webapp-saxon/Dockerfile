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
FROM jetty:9.4.27-jre8

# add the healthcheck
RUN mkdir /var/lib/jetty/webapps/healthcheck && echo "OK" > /var/lib/jetty/webapps/healthcheck/index.html

# port and run command
EXPOSE 8080

# copy the WAR file
COPY --from=builder /build/fcrepo-webapp/fcrepo-webapp-saxon/target/saxon.war /var/lib/jetty/webapps/ROOT.war

#
# end of file
#
