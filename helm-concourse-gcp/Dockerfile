FROM typositoire/concourse-helm3-resource

ENV GCLOUD_SDK_VERSION=297.0.0
ENV GCLOUD_SDK_URL=https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${GCLOUD_SDK_VERSION}-linux-x86_64.tar.gz
ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/google-cloud-sdk/bin

WORKDIR /

RUN apk add --update --no-cache ca-certificates git python jq bash curl tar gzip

RUN mkdir -p /opt \
  && curl -sSL "${GCLOUD_SDK_URL}" | tar zx -C /opt \
  && /opt/google-cloud-sdk/install.sh -q
  
RUN helm plugin install https://github.com/viglesiasce/helm-gcs.git >/dev/null 2>&1