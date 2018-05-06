FROM ricejasonf/cppdock:linux_x64 as boost_libraries
  RUN apt-get update -y && apt-get install wget
  WORKDIR /usr/local/src
  RUN wget https://dl.bintray.com/boostorg/release/1.67.0/source/boost_1_67_0.tar.gz \
    && tar -xvzf boost_1_67_0.tar.gz

  WORKDIR /usr/local/src/boost_1_67_0
  RUN mkdir /opt/install/include \
    && cp -R -t /opt/install/include boost

FROM ricejasonf/cppdock:linux_x64 as metal
  RUN cppdock install_dep linux_x64 \
          d9cf4de59cff8521910175f83fe6d4a9f8a54bf6 brunocodutra/metal

FROM ricejasonf/cppdock:linux_x64 as meta
  RUN cppdock install_dep linux_x64 \
          9780f3527839caa83d8f9ebe43953e067351c40b ericniebler/meta

FROM ricejasonf/cppdock:linux_x64 as kmpl
  RUN cppdock install_dep linux_x64 \
          8bd3e8ccaa7e4f71d8469b391ebde011341e94c4 kvasir-io/mpl

FROM ricejasonf/cppdock:linux_x64 as benchmark

  RUN apt-get update && apt-get install -yq git ruby-dev

  COPY --from=boost_libraries /opt/install /usr/local
  COPY --from=metal /opt/install /usr/local
  COPY --from=meta /opt/install /usr/local
  COPY --from=kmpl /opt/install /usr/local


  WORKDIR /usr/local/src
  RUN git clone --depth 1 \
         https://github.com/ldionne/metabench.git
  WORKDIR /opt/build
  RUN cmake  \
        -DCMAKE_TOOLCHAIN_FILE=/opt/toolchain.cmake \
        /usr/local/src/metabench \
   && cmake --build . --target benchmark
  
  CMD /bin/bash
