FROM dockcross/base:latest
FROM gcc:latest


LABEL maintainer="Matt McCormick matt.mccormick@kitware.com"

RUN apt-get update && \
    apt-get -y install \
    libelf-dev \
    libssl-dev \
    libtbb-dev \
    && apt-get clean --yes

RUN apt-get install nano

ENV CROSS_TRIPLE x86_64-linux-gnu
ENV CROSS_ROOT /usr/bin
ENV AS=/usr/bin/${CROSS_TRIPLE}-as \
    AR=/usr/bin/${CROSS_TRIPLE}-ar \
    CC=/usr/bin/${CROSS_TRIPLE}-gcc \
    CPP=/usr/bin/${CROSS_TRIPLE}-cpp \
    CXX=/usr/bin/${CROSS_TRIPLE}-g++ \
    LD=/usr/bin/${CROSS_TRIPLE}-ld \
    FC=/usr/bin/${CROSS_TRIPLE}-gfortran

COPY ${CROSS_TRIPLE}-noop.sh /usr/bin/${CROSS_TRIPLE}-noop

COPY Toolchain.cmake /usr/lib/${CROSS_TRIPLE}/
ENV CMAKE_TOOLCHAIN_FILE /usr/lib/${CROSS_TRIPLE}/Toolchain.cmake



FROM gcc:latest

COPY . /usr/gcc/cpp_test

WORKDIR /usr/gcc/cpp_test

RUN g++ -o Test HelloWorld.cpp

CMD [ "./Test" ]