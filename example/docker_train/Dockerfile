FROM ricejasonf/cppdock:linux_x64 as linux

    COPY main.cpp /opt/src/
    COPY CMakeLists.txt /opt/src/
    WORKDIR /opt/build
    RUN cmake \
            -DCMAKE_TOOLCHAIN_FILE=/opt/toolchain.cmake \
            -DCMAKE_INSTALL_PREFIX=/opt/install \
            /opt/src \
     && cmake --build . --target train \
     && cmake --build . --target install

FROM ricejasonf/cppdock:emscripten as nodejs

    COPY main.cpp /opt/src/
    COPY CMakeLists.txt /opt/src/
    WORKDIR /opt/build
    RUN cmake \
            -DCMAKE_TOOLCHAIN_FILE=/opt/toolchain.cmake \
            -DCMAKE_INSTALL_PREFIX=/opt/install \
            /opt/src \
     && cmake --build . --target train \
     && cmake --build . --target install

FROM ricejasonf/cppdock:macosx as macosx 

    COPY main.cpp /opt/src/
    COPY CMakeLists.txt /opt/src/
    WORKDIR /opt/build
    RUN cmake \
            -DCMAKE_TOOLCHAIN_FILE=/opt/toolchain.cmake \
            -DCMAKE_INSTALL_PREFIX=/opt/install \
            /opt/src \
     && cmake --build . --target train \
     && cmake --build . --target install


FROM ubuntu:bionic

    COPY --from=linux  /opt/install/ /opt/install
    COPY --from=nodejs /opt/install/ /opt/install

    CMD cp -R /opt/install/* /opt/target/
