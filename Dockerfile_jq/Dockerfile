FROM alpine:3.8

# Install JQ
# Note: Latest version may be found on:
# https://stedolan.github.io/jq/

ARG JQ_VERSION=1.6

ADD https://github.com/stedolan/jq/releases/download/jq-${JQ_VERSION}/jq-linux64 /usr/local/bin/jq

ENV HOME=/config

RUN set -x && \
    apk add --no-cache curl ca-certificates && \
    chmod +x /usr/local/bin/jq && \
    \
    # Create non-root user (with a randomly chosen UID/GUI).
    adduser jquery -Du 2344 -h /config

USER jquery

ENTRYPOINT ["/usr/local/bin/jq"]