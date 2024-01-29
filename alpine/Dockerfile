FROM alpine

ARG GUETZLI_VERSION=1.0.1
ARG GUETZLI_CHECKSUM_SHA256=e52eb417a5c0fb5a3b08a858c8d10fa797627ada5373e203c196162d6a313697

RUN apk add --update --no-cache --virtual .build \
        gflags \
        libpng-dev \
        curl \
        make \
        g++ \
    && apk add --update --no-cache libpng libstdc++ libgcc \
    && curl -L --fail -o /tmp/guetzli.tar.gz \
        https://github.com/google/guetzli/archive/refs/tags/v${GUETZLI_VERSION}.tar.gz \
    && echo "${GUETZLI_CHECKSUM_SHA256}  /tmp/guetzli.tar.gz" > /tmp/guetzli_checksum.txt \
    && sha256sum -w -c /tmp/guetzli_checksum.txt \
    && mkdir /tmp/guetzli \
    && tar -zxv --strip-components=1 -f /tmp/guetzli.tar.gz -C /tmp/guetzli \
    && cd /tmp/guetzli \
    && make \
    && cp bin/Release/guetzli /usr/local/bin/guetzli \
    && rm -f /tmp/guetzli.tar.gz \
    && rm -rf /tmp/guetzli \
    && rm -f /tmp/guetzli_checksum.txt \
    && apk del .build

WORKDIR /guetzli
ENTRYPOINT ["guetzli"]
