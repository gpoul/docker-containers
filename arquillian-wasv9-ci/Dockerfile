FROM ibmcom/websphere-traditional:9.0.0.1-install

MAINTAINER Gerhard Poul <gerhard.poul@gmail.com>

USER root

# Install everything we need for running the tests
RUN apt-get update && apt-get install -y openjdk-8-jdk git maven

# Create a test profile
ARG PROFILE_NAME=AppSrv01
ARG CELL_NAME=DefaultCell01
ARG NODE_NAME=DefaultNode01
ARG HOST_NAME=localhost

RUN /opt/IBM/WebSphere/AppServer/bin/manageprofiles.sh -create -templatePath \
    /opt/IBM/WebSphere/AppServer/profileTemplates/default/ -profileName $PROFILE_NAME \
    -profilePath /opt/IBM/WebSphere/AppServer/profiles/$PROFILE_NAME  \
    -nodeName $NODE_NAME -cellName $CELL_NAME -hostName $HOST_NAME 

# Required because we're testing the V8.5 arquillian container adapter on WAS V9.0
RUN cp /opt/IBM/WebSphere/AppServer/runtimes/com.ibm.ws.admin.client_9.0.jar /opt/IBM/WebSphere/AppServer/runtimes/com.ibm.ws.admin.client_8.5.0.jar

CMD ["/work/start_server"]
