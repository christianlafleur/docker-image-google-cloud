FROM alpine:latest

USER root
ENV USER root

RUN apk update \
    && apk add \
    bash \
    curl \
    git \
    python2 \
    py-pip

# Install Go
RUN curl -o /tmp/go.tar.gz https://storage.googleapis.com/golang/go1.6.4.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf /tmp/go.tar.gz \
    && rm /tmp/go.tar.gz
ENV GOPATH ${HOME}/go
ENV PATH ${PATH}:/usr/local/go/bin

## Install Google Cloud SDK
RUN curl -o /tmp/google-cloud-sdk.tar.gz https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-152.0.0-linux-x86_64.tar.gz \
    && tar -C /usr/local -xzf /tmp/google-cloud-sdk.tar.gz \
    && rm /tmp/google-cloud-sdk.tar.gz \
    && /usr/local/google-cloud-sdk/install.sh --quiet --usage-reporting=false --path-update=true
ENV PATH ${PATH}:/usr/local/google-cloud-sdk/bin

# Opt-out of privacy violations.
RUN gcloud config set disable_usage_reporting true

# Update and install optional components.
RUN gcloud components update \
  && gcloud components install --quiet \
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
  pubsub-emulator

# Install SDKs for Go.
RUN go get \
  google.golang.org/appengine \
  google.golang.org/grpc
