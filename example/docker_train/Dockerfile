FROM ricejasonf/cppdock:linux_x64 as linux

    COPY main.cpp /opt/src/
    COPY CMakeLists.txt /opt/src/
    WORKDIR /opt/build
    RUN cmake -DCMAKE_TOOLCHAIN_FILE=/opt/toolchain.cmake /opt/src \
     && cmake --build . --target train

FROM ricejasonf/cppdock:emscripten as nodejs

    COPY main.cpp /opt/src/
    COPY CMakeLists.txt /opt/src/
    WORKDIR /opt/build
    RUN cmake -DCMAKE_TOOLCHAIN_FILE=/opt/toolchain.cmake /opt/src \
     && cmake --build . --target train

FROM ubuntu:bionic
    RUN apt-get update && apt-get install -yq libc++-dev libc++abi-dev
    COPY --from=linux  /opt/build/train /opt/bin/train
    COPY --from=nodejs /opt/build/train.js /opt/bin/train.js

    CMD ["/opt/bin/train"]
