FROM alpine:latest
MAINTAINER SgrAlpha <admin@mail.sgr.io>

ENV JAVA_HOME=/usr/lib/jvm/java-15-oracle \
    PATH="/usr/lib/jvm/java-15-oracle/bin:$PATH"

RUN GLIBC_VERSION=2.31-r0 && \
    ZLIB_VERSION=1.2.11-4 && \
    JAVA_VERSION=15.0.2 && \
    JAVA_BUILD=7 && \
    JAVA_SIG=0d1cfde4252546c6931946de8db48ee2 && \
    apk --update add --no-cache ca-certificates curl openssl binutils xz && \
    curl -Ls https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub -o /etc/apk/keys/sgerrand.rsa.pub && \
    curl -Ls https://github.com/sgerrand/alpine-pkg-glibc/releases/download/"${GLIBC_VERSION}"/glibc-"${GLIBC_VERSION}".apk \
        -o /tmp/glibc-"${GLIBC_VERSION}".apk && \
    apk add /tmp/glibc-"${GLIBC_VERSION}".apk && \
    mkdir /tmp/zlib && \
    curl -Ls https://archive.archlinux.org/packages/z/zlib/zlib-1%3A"${ZLIB_VERSION}"-x86_64.pkg.tar.xz \
        | tar -xJ -C /tmp/zlib && \
    mv /tmp/zlib/usr/lib/libz.so* /usr/glibc-compat/lib && \
    apk del binutils && \
    curl -Ls --cookie "oraclelicense=accept-securebackup-cookie;" \
        http://download.oracle.com/otn-pub/java/jdk/"${JAVA_VERSION}"+"${JAVA_BUILD}"/"${JAVA_SIG}"/jdk-"${JAVA_VERSION}"_linux-x64_bin.tar.gz \
        | tar xz -C /tmp && \
    mkdir -p /usr/lib/jvm && mv /tmp/jdk-${JAVA_VERSION} "${JAVA_HOME}" && \
    rm -rf /tmp/* /var/cache/apk/*
