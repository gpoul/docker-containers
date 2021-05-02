FROM ibmcom/websphere-traditional:latest

MAINTAINER Gerhard Poul <gerhard.poul@gmail.com>

USER root

# Install everything we need for running the tests
RUN yum install -y java-1.8.0-openjdk-devel git maven

# Create a test profile
ARG PROFILE_NAME=AppSrv01
ARG CELL_NAME=DefaultCell01
ARG NODE_NAME=DefaultNode01
ARG HOST_NAME=localhost

# Remove the profile from the base image and recreate to make sure it's created with the params we want
RUN /opt/IBM/WebSphere/AppServer/bin/manageprofiles.sh -delete -profileName $PROFILE_NAME && rm -rf /opt/IBM/WebSphere/AppServer/profiles/$PROFILE_NAME

RUN /opt/IBM/WebSphere/AppServer/bin/manageprofiles.sh -create -templatePath \
    /opt/IBM/WebSphere/AppServer/profileTemplates/default/ -profileName $PROFILE_NAME \
    -profilePath /opt/IBM/WebSphere/AppServer/profiles/$PROFILE_NAME  \
    -nodeName $NODE_NAME -cellName $CELL_NAME -hostName $HOST_NAME 

CMD ["/work/start_server"]
