FROM almalinux:8

ENV AWS_CLI_VERSION=2.11.15

RUN dnf -y upgrade && \
    dnf -y install unzip openssl git python3 python3-pip jq vim 'dnf-command(config-manager)' && \
    dnf -y module enable nodejs:18 && \
    dnf -y install nodejs && \
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64-${AWS_CLI_VERSION}.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install && \
    rm -rf awscliv2.zip aws && \
    mkdir /root/.aws && \
    npm install -g aws-cdk serverless aws-sdk

ARG AWS_ACCESS_KEY_ID
ARG AWS_SECRET_ACCESS_KEY
ARG AWS_DEFAULT_REGION

RUN echo "[default]" > /root/.aws/config && \
    echo "region = ${AWS_DEFAULT_REGION}" >> /root/.aws/config && \
    echo "output = json" >> /root/.aws/config && \
    echo "[default]" > /root/.aws/credentials && \
    echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}" >> /root/.aws/credentials && \
    echo "aws_secret_access_key = ${AWS_SECRET_ACCESS_KEY}" >> /root/.aws/credentials

ENV SERVERLESS_ACCESS_KEY_ID=""
ENV SERVERLESS_SECRET_ACCESS_KEY=""

RUN serverless config credentials --provider aws --key ${SERVERLESS_ACCESS_KEY_ID} --secret ${SERVERLESS_SECRET_ACCESS_KEY} --profile serverless-admin