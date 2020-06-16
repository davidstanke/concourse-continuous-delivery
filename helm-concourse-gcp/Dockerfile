# adapted from linkyard/concourse-helm-resource

FROM alpine:3.8

ENV HELM_VERSION=3.2.0
ENV KUBECTL_VERSION=1.11.6
ENV GCLOUD_SDK_VERSION=177.0.0

ENV HELM_URL=https://get.helm.sh/helm-v${HELM_VERSION}-linux-amd64.tar.gz
ENV KUBECTL_URL=https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl
ENV GCLOUD_SDK_URL=https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${GCLOUD_SDK_VERSION}-linux-x86_64.tar.gz

ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/google-cloud-sdk/bin

WORKDIR /
RUN apk add --update --no-cache ca-certificates git python jq bash curl tar gzip gettext
RUN curl -sSL -o /usr/local/bin/kubectl "${KUBECTL_URL}" \
  && chmod +x /usr/local/bin/kubectl
RUN mkdir -p /opt \
  && curl -sSL "${GCLOUD_SDK_URL}" | tar zx -C /opt \
  && /opt/google-cloud-sdk/install.sh -q
RUN curl -sSL "${HELM_URL}" | tar zx -C /tmp \
  && mv /tmp/linux-amd64/helm /usr/local/bin/helm \
  && helm plugin install https://github.com/viglesiasce/helm-gcs.git >/dev/null 2>&1

ADD assets /opt/resource
RUN chmod +x /opt/resource/*

ENTRYPOINT [ "/bin/bash" ]
