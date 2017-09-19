FROM debian:stretch-slim as gitclone
LABEL maintainer="toughIQ <toughiq@gmail.com>"

ARG GIT_BRANCH=2.9dev
RUN apt-get update \
    && apt-get install -y --no-install-recommends git openssl ca-certificates
    
RUN git clone -b $GIT_BRANCH https://github.com/drwetter/testssl.sh.git

### Build actual image
FROM debian:stretch-slim
LABEL maintainer="toughIQ <toughiq@gmail.com>"

RUN apt-get update \
    && apt-get install -y --no-install-recommends openssl host procps bsdmainutils \
    && apt-get clean all \
    && rm -rf /var/lib/apt/lists/*

COPY --from=gitclone /testssl.sh /testssl
WORKDIR /testssl
RUN rm -rf /testssl/bin /testssl/doc
ENTRYPOINT ["/testssl/testssl.sh"]
