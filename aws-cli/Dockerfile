From almalinux:8.5
RUN dnf -y upgrade
RUN dnf -y install unzip
RUN dnf -y install openssl
RUN dnf -y install git
RUN dnf -y install python3
RUN dnf -y install python3-pip
RUN dnf -y module enable nodejs:16
RUN dnf -y install nodejs
RUN dnf -y install 'dnf-command(config-manager)'
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip
RUN mkdir /root/.aws
RUN  ./aws/install
ARG AWS_ACCESS_KEY_ID
ARG AWS_SECRET_ACCESS_KEY
ARG AWS_DEFAULT_REGION
ARG SERVERLESS_ACCESS_KEY_ID
ARG SERVERLESS_SECRET_ACCESS_KEY
RUN echo "[default]" > /root/.aws/config
RUN echo "region = ${AWS_DEFAULT_REGION}" >> /root/.aws/config
RUN echo "output = json" >> /root/.aws/config
RUN echo "[default]" > /root/.aws/credentials
RUN echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}" >> /root/.aws/credentials
RUN echo "aws_secret_access_key = ${AWS_SECRET_ACCESS_KEY}" >> /root/.aws/credentials
RUN npm install -g aws-cdk
RUN npm install -g serverless
RUN serverless config credentials --provider aws --key ${SERVERLESS_ACCESS_KEY_ID} --secret ${SERVERLESS_SECRET_ACCESS_KEY} --profile serverless-admin 