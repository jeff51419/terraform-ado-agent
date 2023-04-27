FROM ubuntu:20.04
RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get upgrade -y

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -qq --no-install-recommends \
    apt-transport-https \
    apt-utils \
    ca-certificates \
    curl \
    git \
    iputils-ping \
    jq \
    lsb-release \
    wget \
    unzip \
    ansible \
    software-properties-common

RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

ARG TF_VERSION=1.4.5

# Can be 'linux-x64', 'linux-arm64', 'linux-arm', 'rhel.6-x64'.
ENV TARGETARCH=linux-x64

RUN wget -q https://releases.hashicorp.com/terraform/${TF_VERSION}/terraform_${TF_VERSION}_linux_amd64.zip

RUN unzip terraform_${TF_VERSION}_linux_amd64.zip && mv terraform bin/terraform

RUN apt-get autoclean
RUN rm -rf  terraform_${TF_VERSION}_linux_amd64.zip

WORKDIR /azp

COPY ./start.sh .
RUN chmod +x start.sh

ENTRYPOINT [ "./start.sh" ]