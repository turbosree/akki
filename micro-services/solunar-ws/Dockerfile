FROM alpine:3.12
RUN apk add git build-base tzdata zlib-dev && \
    wget https://ftp.gnu.org/gnu/libmicrohttpd/libmicrohttpd-latest.tar.gz && \
    tar xfvz libmicrohttpd-latest.tar.gz && \
    (cd libmi*; ./configure; make install) && \
    git clone https://github.com/turbosree/solunar_ws.git && \
    make -C solunar_ws
    # Binary solunar_ws ends up in / directory

FROM alpine:3.12
RUN apk add tzdata
COPY --from=0 /solunar_ws/solunar_ws /
COPY --from=0 /usr/local/lib/libmicrohttpd.so.12 /usr/local/lib
USER 1000
CMD ["/solunar_ws"]
