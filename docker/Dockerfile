FROM ubuntu:latest

USER root
ENV USER root

RUN apt-get update \
    && apt-get install -y \
    curl \
    git \
    python-pip \
    python2.7 \
    && rm -rf /var/lib/apt/lists/*

# Install Go
RUN curl -o /tmp/go.tar.gz https://storage.googleapis.com/golang/go1.6.4.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf /tmp/go.tar.gz \
    && rm /tmp/go.tar.gz \
    && echo "export PATH=$PATH:/usr/local/go/bin;" > /etc/profile \
    && echo "export GOPATH=$HOME/go;" > /etc/profile
ENV PATH $PATH:/usr/local/go/bin
ENV GOPATH $HOME/go

## Install Google Cloud SDK
RUN curl -o /tmp/google-cloud-sdk.tar.gz https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-152.0.0-linux-x86_64.tar.gz \
    && tar -C /usr/local -xzf /tmp/google-cloud-sdk.tar.gz \
    && rm /tmp/google-cloud-sdk.tar.gz \
    && /usr/local/google-cloud-sdk/install.sh --quiet --usage-reporting=false --path-update=true
ENV PATH $PATH:/usr/local/google-cloud-sdk/bin

# Opt-out of privacy violations.
RUN gcloud config set disable_usage_reporting true

# Install optional components and packages.
RUN gcloud components install --quiet \
  alpha \
  app-engine-go \
  app-engine-java \
  app-engine-python \
  beta \
  bq \
  cbt \
  cloud-datastore-emulator \
  core \
  datalab \
  docker-credential-gcr \
  emulator-reverse-proxy \
  gcd-emulator \
  gcloud \
  gsutil \
  kubectl \
  pubsub-emulator \
  && go get \
  google.golang.org/appengine \
  google.golang.org/grpc
