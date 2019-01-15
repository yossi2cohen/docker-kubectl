FROM alpine:3.8

# Install kubectl
# Note: Latest version may be found on:
# https://aur.archlinux.org/packages/kubectl-bin/
# ADD https://storage.googleapis.com/kubernetes-release/release/v1.6.4/bin/linux/amd64/kubectl /usr/local/bin/kubectl

# detect the latest version via: curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt
ARG KUBECTL_VERSION=v1.13.2

ADD https://storage.googleapis.com/kubernetes-release/release/$KUBECTL_VERSION/bin/linux/amd64/kubectl  /usr/local/bin/kubectl

ENV HOME=/config

RUN set -x && \
    apk add --no-cache curl ca-certificates && \
    chmod +x /usr/local/bin/kubectl && \
    \
    # Create non-root user (with a randomly chosen UID/GUI).
    adduser kubectl -Du 2342 -h /config && \
    \
    # Basic check it works.
    kubectl version --client

USER kubectl

RUN mkdir -p ~/.kube
RUN chown kubectl ~/.kube

ENTRYPOINT ["/usr/local/bin/kubectl"]
