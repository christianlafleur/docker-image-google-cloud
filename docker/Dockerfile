FROM ubuntu:latest

USER root
ENV USER root

RUN apt-get update
RUN apt-get install -y apt-utils apt-transport-https
RUN apt-get install -y curl python2.7 python-pip

# Install Go
RUN curl -o /tmp/go.tar.gz https://storage.googleapis.com/golang/go1.6.4.linux-amd64.tar.gz
RUN tar -C /usr/local -xzf /tmp/go.tar.gz
RUN rm /tmp/go.tar.gz
RUN echo "export PATH=$PATH:/usr/local/go/bin"

## Install Google Cloud SDK
RUN curl -o /tmp/google-cloud-sdk.tar.gz https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-152.0.0-linux-x86_64.tar.gz
RUN tar -C /usr/local -xzf /tmp/google-cloud-sdk.tar.gz
RUN rm /tmp/google-cloud-sdk.tar.gz
RUN /usr/local/google-cloud-sdk/install.sh

# Update and install optional components.
RUN gcloud components install datalab core gsutil app-engine-go cbt gc-emulator emulator-reverse-proxy docker-credential-gcr app-engine-java kubectl bq cloud-datastore-emulator pubsub-emulator gcloud alpha beta app-engine-python
