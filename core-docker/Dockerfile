FROM ubuntu:xenial as builder

ENV STELLAR_CORE_VERSION 9.2.0-551-7561c1d5
ENV BUILD_FROM_SRC 0

ADD apt-build /
RUN ["chmod", "+x", "/apt-build"]
RUN /apt-build

ADD install.sh /
RUN chmod +x /install.sh
RUN /install.sh

# -----------------------
FROM ubuntu:xenial

COPY --from=builder /usr/local/bin/stellar-core /usr/local/bin/stellar-core

ADD dependencies /
RUN ["chmod", "+x", "/dependencies"]
RUN /dependencies

RUN ["mkdir", "-p", "/opt/stellar"]

ADD build-config /usr/bin/build-config
RUN ["chmod", "+x", "/usr/bin/build-config"]

ADD launch.sh /
RUN ["chmod", "+x", "/launch.sh"]

ADD configs /configs

ADD entry.sh /
RUN ["chmod", "+x", "/entry.sh"]

EXPOSE 11625
EXPOSE 11626

ENTRYPOINT ["/entry.sh" ]
