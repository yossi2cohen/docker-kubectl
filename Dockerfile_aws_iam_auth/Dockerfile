FROM alpine:3.8

# Download the Amazon EKS-vended aws-iam-authenticator binary from Amazon S3

ARG AWS_IAM_AUTHENTICATOR_VERSION=1.11.5

ADD https://amazon-eks.s3-us-west-2.amazonaws.com/${AWS_IAM_AUTHENTICATOR_VERSION}/2018-12-06/bin/linux/amd64/aws-iam-authenticator /usr/local/bin/aws-iam-authenticator

ENV HOME=/config

RUN set -x && \
    apk add --no-cache curl ca-certificates && \
    chmod +x /usr/local/bin/aws-iam-authenticator && \
    \
    # Create non-root user (with a randomly chosen UID/GUI).
    adduser aws-iam-authenticator -Du 2343 -h /config && \
    \
    # Basic check it works.
    aws-iam-authenticator help

USER aws-iam-authenticator

RUN mkdir -p ~/.aws
RUN chown aws-iam-authenticator ~/.aws

ENTRYPOINT ["/usr/local/bin/aws-iam-authenticator"]