FROM ricejasonf/cppdock:linux_x64

COPY main.cpp /opt/build/

WORKDIR /opt/build

RUN clang++ -stdlib=libc++ -lc++abi main.cpp

CMD ["./a.out"]
