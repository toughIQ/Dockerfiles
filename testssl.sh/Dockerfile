FROM debian:stretch-slim as gitclone
LABEL maintainer="toughIQ <toughiq@gmail.com>"

RUN apt-get update \
    && apt-get install -y --no-install-recommends git openssl ca-certificates
    
RUN git clone -b 2.9dev https://github.com/drwetter/testssl.sh.git

### Build actual image
FROM debian:stretch-slim
LABEL maintainer="toughIQ <toughiq@gmail.com>"

RUN apt-get update \
    && apt-get install -y --no-install-recommends openssl host procps bsdmainutils \
    && apt-get clean all \
    && rm -rf /var/lib/apt/lists/*


COPY --from=gitclone /testssl.sh /testssl
WORKDIR /testssl
ENTRYPOINT ["/testssl/testssl.sh"]
