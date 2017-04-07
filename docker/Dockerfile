FROM ubuntu:xenial
ENV CLOUD_SDK_REPO "cloud-sdk-xenial"

USER root
ENV USER root

RUN apt-get update
RUN apt-get install -y apt-utils apt-transport-https
RUN apt-get install -y curl python2.7 python-pip

## Install Google Cloud SDK
# Create an env var for the correct distribution of Google Cloud SDK.
# Add the Cloud SDK distribution URI as a package source
RUN echo "deb https://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
# Import the Google Cloud public key
RUN curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
# Update and install the Cloud SDK with optional components.
RUN apt-get update
RUN apt-get install -y google-cloud-sdk google-cloud-sdk-app-engine-python google-cloud-sdk-app-engine-java google-cloud-sdk-datalab google-cloud-sdk-datastore-emulator google-cloud-sdk-pubsub-emulator google-cloud-sdk-bigtable-emulator kubectl

# Install App Engine extensions for Python.
RUN gcloud components install app-engine-python
RUN gcloud components install app-engine-python-extras

# Initialize
RUN gcloud init
