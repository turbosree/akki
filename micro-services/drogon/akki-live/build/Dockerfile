FROM ubuntu:18.04

RUN apt-get update -yqq \
    && apt-get install -yqq --no-install-recommends software-properties-common \
    sudo curl wget cmake pkg-config locales git gcc-8 g++-8 build-essential \
    openssl libssl-dev libjsoncpp-dev uuid-dev zlib1g-dev libc-ares-dev\
    postgresql-server-dev-all libmariadbclient-dev libsqlite3-dev \
    && rm -rf /var/lib/apt/lists/* \
    && locale-gen en_US.UTF-8

WORKDIR /app

RUN git clone https://github.com/an-tao/drogon && \ 
    cd drogon && \
    git submodule update --init && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make && make install

ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8 \
    CC=gcc-8 \
    CXX=g++-8 \
    AR=gcc-ar-8 \
    RANLIB=gcc-ranlib-8 \
    BOOST_INCLUDE_DIR="${HOME}/opt/boost_1_67_0" \  
    IROOT=/install
ARG DEBIAN_FRONTEND=noninteractive

COPY akki-live /app
RUN ls -la /
RUN ls -la /app
RUN chmod u+x /app/akki-live
WORKDIR /app

# Run the process with a non-root user
USER 1000
ENTRYPOINT ["./akki-live"]
CMD ["--urls", "http://0.0.0.0:8080"]

