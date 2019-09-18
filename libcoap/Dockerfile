From ubuntu:18.04


RUN apt-get update && apt-get install -y \
    build-essential \
    autoconf \
    automake \
    libtool \
    libtool-bin \
    pkg-config \
    git

RUN git clone https://github.com/obgm/libcoap
WORKDIR /libcoap
# init tinydtls submodule
RUN git submodule init && git submodule update
# start build
RUN ./autogen.sh --clean && ./autogen.sh
RUN ./configure --disable-documentation --enable-examples --with-tinydtls --disable-shared && \
    make install clean


# define some variable
ENV SECRET secretPSK
# RUN "echo ${SECRET}"

EXPOSE 5683:5683/udp
EXPOSE 5684:5684/udp

CMD ["coap-server", "-k", "secretPSK", "-v", "10", "coaps://[::]"]
