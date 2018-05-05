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

FROM ricejasonf/cppdock:tvossimulator as osx

    COPY main.cpp /opt/src/
    COPY CMakeLists.txt /opt/src/
    WORKDIR /opt/build
    RUN cmake -DCMAKE_TOOLCHAIN_FILE=/opt/toolchain.cmake /opt/src \
     && cmake --build . --target train

FROM scratch
    COPY --from=linux  /opt/build/train /opt/bin/train.linux
    COPY --from=nodejs /opt/build/train /opt/bin/train.js
    COPY --from=osx    /opt/build/train /opt/bin/train.osx

    VOLUME /opt/bin

    CMD ["/opt/bin/train.linux"]
